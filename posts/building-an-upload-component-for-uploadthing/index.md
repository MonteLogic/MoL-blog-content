---
title: "Building an Upload Component for uploadthing"
date: "2023-07-25"
---

I guess I just have to figure out how to post to imageUploader from, 'src/server/uploadthing.ts'.

```
// FileRouter for your app, can contain multiple FileRoutes
export const ourFileRouter = {
  // Define as many FileRoutes as you like, each with a unique routeSlug
  imageUploader: f({ image: { maxFileSize: "8MB" } })
    // Set permissions and file types for this FileRoute
    .middleware(async ({ req, res }) => {
      // This code runs on your server before upload
      const user = await auth(req, res);
 
      // If you throw, the user will not be able to upload
      if (!user) throw new Error("Unauthorized");
 
      // Whatever is returned here is accessible in onUploadComplete as `metadata`
      return { userId: user.id };
    })
    .onUploadComplete(async ({ metadata, file }) => {
      // This code RUNS ON YOUR SERVER after upload
      console.log("Upload complete for userId:", metadata.userId);
 
      console.log("file url", file.url);
    }),
} satisfies FileRouter;
```

I am going to try to get rid of the generate component block logic and import each manually.

Okay, I rewrote the component to:

```
import { UploadButton } from "@uploadthing/react"
// You need to import our styles for the button to look right. Best to import in the root /_app.tsx but this is fine
import "@uploadthing/react/styles.css";
 
export default function Home() {
  return (
    <main className="flex min-h-screen flex-col items-center justify-between p-24">
      <UploadButton
        endpoint="imageUploader"
        onClientUploadComplete={(res) => {
          // Do something with the response
          console.log("Files: ", res);
          alert("Upload Completed");
        }}
        onUploadError={(error: Error) => {
          // Do something with the error.
          alert(`ERROR! ${error.message}`);
        }}
      />
    </main>
  );
}
```

This is the only example I found which I can fanaggle it.

```
import { UploadDropzone } from "~/utils/uploadthing";
// You need to import our styles for the button to look right. Best to import in the root /_app.tsx but this is fine
import "@uploadthing/react/styles.css";

export default function Home() {
  return (
    <main className="flex min-h-screen flex-col items-center justify-between p-24">


      <UploadDropzone
        endpoint="imageUploader"
        onClientUploadComplete={(res) => {
          // Do something with the response
          console.log("Files: ", res);
          alert("Upload Completed");
        }}
        onUploadError={(error: Error) => {
          alert(`ERROR! ${error.message}`);
        }}
      />
    </main>
  );
}


```

A list of components to be used, [link](https://github.com/pingdotgg/uploadthing/blob/11c5ab317203c5e13253bd90c6d57075feaed06f/packages/react/src/component.tsx).

I need to post to this [URL](http://localhost:3000/api/uploadthing?actionType=upload&slug=imageUploader).

I just need to figure out how to write a custom component which uses useUploadThing to reduce the size of the component.

...

This [file](https://github.com/miljan-code/modern-blog/blob/8b235faf1737f2f4c0decdbb203df6d7a09886d7/components/upload-dropzone.tsx#L20) has promise.

...

I don't think I was using ourFileRouter when I should have.

This works an uploader for uploadthing, [gist](https://gist.github.com/MonteLogic/9a1b143bea8ff6c6955fd4684f0a038d).

I am going to use something like this [gist](https://gist.github.com/MonteLogic/acf87a4652156ef6f7701e6ca51edd40) style of code to trigger the event of uploading the image. So I'm going to upload the image by pressing a button on AddReceipt and the MultiUploader function will run it's code as well.

...

I'm not against comparing this to, Vercel's file storage service.

...

I need to get rid of the upload button on the dropzone as it becomes redundant and makes the component confusing.

// I need to pass in an onComplete method for when the image has completed the upload process to the server.

This [file](https://github.com/hayato94087/next-uploadthing-sample/blob/main/src/app/customUploadButtonSample.tsx) is good too.

Okay now that I got the file upload good, I have to trace it back and save it(to the db), also I would like to have the form cleared and have the image uploaded added asynchronously to the dom.

...

I also really need to add the date which the entry was submitted to the database.

Something like, [this](https://codesandbox.io/s/quirky-tharp-or0qip?file=/src/App.js) could be used as a modal window for mobile a .tsx version [here](https://github.com/emilkowalski/vaul/tree/main).

I notice if the page isn't getting refreshed the db receives a value from the time it was first refreshed not when it was REALLY sent out.

So I deployed the app but it's having issues connecting to prisma.

```
PrismaClientInitializationError: 
Invalid `prisma.trucks.findMany()` invocation:


Error querying the database: unable to open database file: /var/task/node_modules/.prisma/client/./dev.db
    at An.handleRequestError (/var/task/node_modules/@prisma/client/runtime/library.js:174:7205)
    at An.handleAndLogRequestError (/var/task/node_modules/@prisma/client/runtime/library.js:174:6358)
    at /var/task/node_modules/@prisma/client/runtime/library.js:177:2908
    at async /var/task/node_modules/@prisma/client/runtime/library.js:177:3123
    at async t._executeRequest (/var/task/node_modules/@prisma/client/runtime/library.js:177:10621)
    at async getServerSideProps (/var/task/.next/server/pages/index.js:69:20) {
  clientVersion: '4.15.0',
  errorCode: undefined,
  page: '/en'
}
RequestId: 390c7b8d-f467-444f-b447-a94cf7fd32ab Error: Runtime exited with error: exit status 1
Runtime.ExitError
```
