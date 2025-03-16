---
title: "Work Notes: Creating a custom WordPress API to interact frontend with the backend."
date: "2023-02-21"
---

I would like to make a control panel of what components to render on the frontend but I can't get the attributes on the frontend with the ease I would like.

I should be able to post to the API in the editor using privileged credentials. And the API will be able to be viewed from the frontend.

```
function my_awesome_api_route() {
    register_rest_route( 'myapi/v1', '/posts', array(
        'methods'  => 'GET',
        'callback' => 'my_awesome_api_callback',
    ) );
}

function my_awesome_api_callback( $request ) {
    $args = array(
        'post_type' => 'post',
        'posts_per_page' => -1,
    );
    $query = new WP_Query( $args );
    $posts = array();
    while ( $query->have_posts() ) {
        $query->the_post();
        $posts[] = array(
            'title' => get_the_title(),
            'content' => get_the_content(),
        );
    }
    wp_reset_postdata();
    return $posts;
}

add_action( 'rest_api_init', 'my_awesome_api_route' );
```

Post to that API with JavaScript:

```
const data = {
    title: 'My new post',
    content: 'This is the content of my new post',
};

fetch('/wp-json/myapi/v1/posts', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(data),
})
.then(response => {
    console.log('Success:', response);
})
.catch(error => {
    console.error('Error:', error);
});
```

Having a tough time getting the POST method to work.

Reading this:

https://stackoverflow.com/questions/41362277/wp-rest-api-custom-end-point-post-request

The console.log, is showing what I want but it's not changing it.

Looking at examples:

https://github.com/imranhsayed/rest-api-endpoints

I just realized I tried to use 'POST' to update the existing values of an API. 'PUT' is appropriate for this.

For some reason the boolean values are changing to "1" rather than true--within the database.

Having issues with permission\_callback. May use this:

I included this as a check and it worked.

```

add_filter( 'rest_authentication_errors', function( $result ) {
    // Check if the current request is a PUT request to your API endpoint
    if ( $_SERVER['REQUEST_METHOD'] === 'PUT' && strpos( $_SERVER['REQUEST_URI'], '/my-api/v1/my-boolean-values' ) !== false ) {
        // Check if the current user has the 'edit_posts' capability
        if ( ! current_user_can( 'edit_posts' ) ) {
            // If the user is not authorized, return an error message
            return new WP_Error( 'rest_forbidden', __( 'You are not authorized to make this request.', 'my-text-domain' ), array( 'status' => 401 ) );
        }
    }
    // If the request is not a PUT request to your API endpoint, return the original result
    return $result;
} );

```

Now, I'm just testing if custom block conditionally rendered logic will work.

For some reason the conditional logic returns only works well if you do it like this:

```
export const DatePicker = () => {
    const [value1, setValue1] = useState(false);
    const [value2, setValue2] = useState(false);
    const [value3, setValue3] = useState(false);

    useEffect(() => {
        fetch('/wp-json/my-api/v1/my-boolean-values')
            .then(response => response.json())
            .then(data => {
                setValue1(data.value1);
                setValue2(data.value2);
                setValue3(data.value3);
            });
    }, []);


    return (
        <div>
            {value3 ?  (
                    <div>The card message will render here.</div>
            ) : null 
        }
        </div>
    );
};
```

...

Adding the control panel while observing the documentation.

https://developer.wordpress.org/block-editor/reference-guides/components/toggle-control/

For the ToggleControl, I could make the put request based on the value of an attribute. I want to get the solution done quickly but I know performant code within http requests is very important.

For some reason the useEffect value for my ToggleControl does not want to equal false. To fix this you must make it only boolean and a default in the block.json no other qualifiers of the attribute.
