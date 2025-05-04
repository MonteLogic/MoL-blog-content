---
title: "Work Notes: Uploading multiple images via UploadThing"
date: "2023-08-09"
---

The code I currently have only allows for uploading one image.

This [repo](https://github.com/t3dotgg/imgmanager) shows multiple images being uploaded, it also lint-free.

I am focusing on this block of code from imgmanager which appears to upload multiple files:

```
  useEffect(() => {
    if (props.upload) {
      uploadFiles({ files: [props.file], endpoint: "imageUploader" }).then(
        () => {
          startTransition(() => {
            props.removeImage();
            refresh();
          });
        }
      );
    }

    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [props.file.name, props.upload]);
```

That request does multiple calls so if it wants to send two images then it sends two post requests.

This is currently what I have to upload just one image:

```

    const { startUpload, isUploading } = useUploadThing("imageUploader", {
        onClientUploadComplete: (res) => {
            console.log("Files: ", res);
            if (res) {
                formData.img = res[0]?.fileUrl as string;
            }

            alert("uploaded successfully and formData.img =" + formData.img);
        },
        onUploadError: (e) => {
            console.log(e);
            console.log(isUploading);
            alert("error occurred while uploading");
        },
    });
```

...

This is the type definition for multiple files:

```
    readonly uploadFiles: (opts: { [TEndpoint_1 in keyof TRouter]: {
        endpoint: TEndpoint_1;
        onUploadProgress?: (({ file, progress, }: {
            file: string;
            progress: number;
        }) => void) | undefined;
        input?: inferEndpointInput<TRouter[TEndpoint_1]> | undefined;
        files: File[];
    }; }[keyof TRouter], config?: {
        url?: string | undefined;
    } | undefined) => Promise<{
        fileUrl: string;
        fileKey: string;
    }[]>;
```

I guess you can upload multiple via the upload button like [this](https://github.com/pingdotgg/uploadthing/pull/48/commits/6b9aba64943c2f060349fe5aec01f713b7381768).

It's just this:

```
    imageUploader: f({ image: { maxFileSize: "4MB", maxFileCount: 10 } })
```

Why the param of UploadButton says multiple but can't be accessed is something I've yet to figure out.

Summary:

Just add a second parameter to the imageUploader functions with the maxfilecount and then you should be able to upload multiple images.
