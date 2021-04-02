# echoAR & A-Frame Demo 

This is a very short & fun tutorial to demonstrate how to use echoAR in [A-Frame](https://aframe.io/) (an widely-used open-source web framework). What do we end up with? An AR application that can run on almost all existing platforms (even on older phones) without using any third party apps.

## Register
If you don't have an echoAR API key yet, make sure to register for FREE at [echoAR](https://console.echoar.xyz/#/auth/register).

## Useful Links

First of all, let's start with a few tutorials:

[HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started): In case you haven't used HTML for a while, here's a refresher.

[A-Frame](https://aframe.io/docs/1.2.0/introduction/): After reading this tutorial, you'll have an idea about what A-Frame is and how to use it. We'll need [Introduction](https://aframe.io/docs/1.2.0/introduction/), [Installation](https://aframe.io/docs/1.2.0/introduction/installation.html), and [Entity-Component-System](https://aframe.io/docs/1.2.0/introduction/entity-component-system.html) for this tutorial, but feel free to dive deeper.

[echoAR Object](https://docs.echoar.xyz/objects) and [API](https://docs.echoar.xyz/queries): we'll use API calls to access files on your echoAR console. Make sure you read them all before we get started.

## Get Started with A-Frame
A simple A-Frame project can be a single HTML file no longer than 10 lines:
```
<html>
  <head>
    <script src="https://aframe.io/releases/1.2.0/aframe.min.js"></script>
  </head>
  <body>
    <a-scene>
      <a-box position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9"></a-box>
    </a-scene>
  </body>
</html>
```
You can add more objects inside the a-scene if you want. After opening the file, you will see a blue box in your browser:

![alt text](./Screenshots/cube.png)

Now we are ready to look at how to use echoAR in A-Frame.

## A Look into the echoAR API Calls
Assuming that you have "Skyscraper.obj" on your console, like this:

![alt text](./Screenshots/console.png)

You can use 
```
https://console.echoAR.xyz/query?key=<API_KEY>
```
to retrieve a data set of entries associated with your API key. Read more about API calls [here](https://docs.echoar.xyz/objects).

You should use Postman and try it out yourself. Using the GET method, you'll see something like this:
![alt text](./Screenshots/postman.png)

In "additionalData", you'll see "glbHologramStorageID". We will need it to retrieve the GLB file. Note that A-Frame supports GLB best, and file formats like OBJ may cause problems including missing texture (since file structures may be different).

To download a file stored in the system, use
```
https://console.echoAR.xyz/query?key=<API_KEY>&file=<FILE_STORAGE_ID>
```
In this case, my API key is "crimson-sky-7281" and the "glbHologramStorageID" of "Skyscraper.obj" is "d686a655-e800-430d-bfd2-e38cdfb0c9e9.glb". Thus, I use this query to get the GLB file:
```
https://console.echoar.xyz/query?key=crimson-sky-7281&file=d686a655-e800-430d-bfd2-e38cdfb0c9e9.glb
```

## Almost Done!
With these two queries, you can create an A-Frame entity like this to use your echoAR objects:
```
<a-entity 
    gltf-model="url(<YOUR_GLB_FILE_QUERY>)"
    position='0 0 0' 
    scale = '0.05 0.05 0.05'
    rotation = "0 -90 0"
</a-entity>
```

Here, I used three few Star Wars themed objects: 
<p float="left">
  <img src="./Screenshots/glb_1.png" width="210" />
  <img src="./Screenshots/glb_2.png" width="210" /> 
  <img src="./Screenshots/glb_3.png" width="210" />

and the code looks like this:

```
<html>
  <head>
    <script src="https://aframe.io/releases/1.2.0/aframe.min.js"></script>
  </head>

  <body>
    <a-scene>
      <!-- Storm Troopers -->
      <a-entity gltf-model="url(https://console.echoar.xyz/query?key=crimson-sky-7281&file=e51e54c3-c14c-4d67-b69f-2fe2ef7973c5.glb)" position = '-1.2 1.5 -5' scale = '2 2 2'></a-entity>
      <!-- R2D2 -->
      <a-entity gltf-model="url(https://console.echoar.xyz/query?key=crimson-sky-7281&file=6ddab898-f190-41cf-9a1a-e06499083db3.glb)" position = '-0.05 1.52 0.2' scale = '0.01 0.01 0.01' rotation = "0 90 0"></a-entity>
      <!-- BB-8 -->
      <a-entity gltf-model="url(https://console.echoar.xyz/query?key=crimson-sky-7281&file=98e0a92e-8598-4afd-a925-d6f273a194db.glb)" position = '0.04 1.4 0.18' scale = '0.1 0.1 0.1' rotation = "0 -90 0"></a-entity>
      
      <!-- Ground -->
      <a-plane position="0 0 0" rotation="-90 0 0" width="1000" height="1000" color="#641E16"></a-plane>
      
      <!-- Sky -->
      <a-sky color="#CD6155"></a-sky>
    </a-scene>
  </body>
</html>
```

## Run
Now, simply click on ```home.html``` to to view the scene in your browser.

There you go!

![alt text](./Screenshots/1.png)
![alt text](./Screenshots/2.png)

## Debug
If you can't see your object, your 3D object is most definitely too large. In this case, try to downsize the object.

## Support
Feel free to reach out at [support@echoAR.xyz](mailto:support@echoAR.xyz) or join our [support channel on Slack](https://join.slack.com/t/echoar/shared_invite/enQtNTg4NjI5NjM3OTc1LWU1M2M2MTNlNTM3NGY1YTUxYmY3ZDNjNTc3YjA5M2QyNGZiOTgzMjVmZWZmZmFjNGJjYTcxZjhhNzk3YjNhNjE). 