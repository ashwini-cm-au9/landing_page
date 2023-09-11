
Primary Menu
amCharts
Products
Demos
Download
Buy
Support
Docs
Find us on
Previous All demos Next
Open in:
Map with Sized Pin Bullets
This demo implements pin-like bullets with the pin head size adjusted based on the corresponding value.

Key implementation details
We are working with bullets on a map point series. We create a Container which is a composite of the parts of our pin. We adjust the pin head radius based on the data item’s value and create a Circle in the container with that radius and vertically offset it accordingly. Then we create a Line for the pin pole and a Label. Finally, we set our composite container as the sprite for our Bullet.

Related tutorials
Map point series
Bullets
Containers
Demo source
JavaScript
TypeScript / ES6
...
/* Imports */



import am4geodata_continentsLow from "@amcharts/amcharts4-geodata/continentsLow";
import am5themes_Animated from "@amcharts/amcharts5/themes/Animated";

/* Chart code */
// Create root and chart
let root = am5.Root.new("chartdiv"); 

// Set themes
root.setThemes([
  am5themes_Animated.new(root)
]);


// ====================================
// Create map
// ====================================

let map = root.container.children.push(
  am5map.MapChart.new(root, {
    panX: "none",
    projection: am5map.geoNaturalEarth1()
  })
);

// Create polygon series
let polygonSeries = map.series.push(
  am5map.MapPolygonSeries.new(root, {
    geoJSON: am5geodata_continentsLow,
    exclude: ["antarctica"],
    fill: am5.color(0xbbbbbb)
  })
);

let pointSeries = map.series.push(
  am5map.MapPointSeries.new(root, {})
);

let colorSet = am5.ColorSet.new(root, {step:2});

pointSeries.bullets.push(function(root, series, dataItem) {
  let value = dataItem.dataContext.value;

  let container = am5.Container.new(root, {});
  let color = colorSet.next();
  let radius = 15 + value / 20 * 20;
  let circle = container.children.push(am5.Circle.new(root, {
    radius: radius,
    fill: color,
    dy: -radius * 2
  }))

  let pole = container.children.push(am5.Line.new(root, {
    stroke: color,
    height: -40,
    strokeGradient: am5.LinearGradient.new(root, {
      stops:[
        { opacity: 1 },
        { opacity: 1 },
        { opacity: 0 }
      ]
    })
  }));

  let label = container.children.push(am5.Label.new(root, {
    text: value + "%",
    fill: am5.color(0xffffff),
    fontWeight: "400",
    centerX: am5.p50,
    centerY: am5.p50,
    dy: -radius * 2
  }))

  let titleLabel = container.children.push(am5.Label.new(root, {
    text: dataItem.dataContext.title,
    fill: color,
    fontWeight: "500",
    fontSize: "1em",
    centerY: am5.p50,
    dy: -radius * 2,
    dx: radius
  }))
 
  return am5.Bullet.new(root, {
    sprite: container
  });
});




// ====================================
// Create pins
// ====================================

let data = [{
  "title": "United States",
  "latitude": 39.563353,
  "longitude": -99.316406,
  "width": 100,
  "height": 100,
  "value":12
}, {
  "title": "European Union",
  "latitude": 50.896104,
  "longitude": 19.160156,
  "width": 50,
  "height": 50,
  "value":15
}, {
  "title": "Asia",
  "latitude": 47.212106,
  "longitude": 103.183594,
  "width": 80,
  "height": 80,
  "value":8  
}, {
  "title": "Africa",
  "latitude": 11.081385,
  "longitude": 21.621094,
  "width": 50,
  "height": 50,
  "value":5
}];

for (var i = 0; i < data.length; i++) {
  let d = data[i];
  pointSeries.data.push({
    geometry: { type: "Point", coordinates: [d.longitude, d.latitude] },
    title: d.title,
    value: d.value
  });
}

amCharts
More info
Accessibility Features
About amCharts
Press Kit
Getting support
Subscribe to amNews
Products
amCharts 5: Charts
amCharts 5: Maps
amCharts 5: Stock Chart
WordPress Plugin 
Version information
Tools & Resources
Free SVG Maps
Pixel Map Generator
Visited Countries Map
Visited States Map
Contact Us
contact@amcharts.com
Support Center
Reporting a vulnerability
Legal Stuff
Privacy Policy
Terms & Conditions
Facebook
Twitter
LinkedIn
Copyright © 2006-2023, amCharts. All rights reserved.


/ Create a chart instance
var chart = am4core.create("chartdiv", am4maps.MapChart);

// Set the map definition (e.g., "worldLow" for a world map)
chart.geodata = am4geodata_worldLow;

// Set the projection
chart.projection = new am4maps.projections.Miller();

// Create map polygon series for the flight route
var series = chart.series.push(new am4maps.MapPolygonSeries());
series.useGeodata = true;

// Add flight route data (you should replace this with your own data)
series.data = [
  {
    "id": "line1",
    "multiGeoLine": [
      [
        {"latitude": startLatitude, "longitude": startLongitude},
        {"latitude": endLatitude, "longitude": endLongitude}
      ]
    ]
  }
];

// Create a map image series for the pin/bullet
var imageSeries = chart.series.push(new am4maps.MapImageSeries());

// Create a map image
var image = imageSeries.mapImages.template.createChild(am4core.Image);
image.propertyFields.href = "image"; // Set the URL of your pin/bullet image
image.propertyFields.latitude = "latitude"; // Set the latitude of the location
image.propertyFields.longitude = "longitude"; // Set the longitude of the location
imageSeries.data = [
  {
    "image": "path/to/your/image.png",
    "latitude": locationLatitude,
    "longitude": locationLongitude
  }
];

// Customize the pin/bullet appearance if needed
image.width = 30;
image.height = 30;
image.tooltipText = "Your Tooltip Text"; // Optional tooltip

// Add zoom control
chart.zoomControl = new am4maps.ZoomControl();

// Enable pan and zoom
chart.seriesContainer.draggable = true;
chart.seriesContainer.resizable = true;

// Finally, make the chart responsive
chart.responsive.enabled = true;

var customMarker = chart.series.push(new am4maps.MapImageSeries());
var marker = customMarker.mapImages.template.createChild(am4core.Image);
marker.width = 30; // Set the width of your image
marker.height = 30; // Set the height of your image
marker.href = "path/to/your/image.png"; // Replace with the path to your image
marker.nonScaling = true; // This ensures the image size doesn't change with zooming
marker.tooltipText = "{title}"; // Customize the tooltip as needed


var image = customMarker.createChild(am4core.MapImage);
image.latitude = latitude; // Replace with the latitude of your location
image.longitude = longitude; // Replace with the longitude of your location
image.tooltipText = "Your Location"; // Customize the tooltip for this specific marker
image.nonScaling = true;

// Create the map chart
var chart = am4core.create("chartdiv", am4maps.MapChart);

// Set the map projection and other properties as needed

// Create custom markers for locations
var customMarker = chart.series.push(new am4maps.MapImageSeries());
var marker = customMarker.mapImages.template.createChild(am4core.Image);
marker.width = 30;
marker.height = 30;
marker.href = "path/to/your/image.png";
marker.nonScaling = true;

// Create and configure a location marker
var image = customMarker.createChild(am4core.MapImage);
image.latitude = latitude; // Replace with the latitude of your location
image.longitude = longitude; // Replace with the longitude of your location
image.tooltipText = "Your Location";

// Configure flight routes using MapLineSeries or other appropriate series

// Finally, don't forget to call chart.dispose() when done to free up resources



// Example of defining an Image Series
var imageSeries = chart.series.push(new am4maps.MapImageSeries());

// Example of creating an image element
var image = imageSeries.mapImages.template.createChild(am4core.Image);


// Example of setting the image source
image.propertyFields.href = "imageURL"; // imageURL is a field in your data containing image URLs

// Example of setting the location
imageSeries.mapImages.template.propertyFields.latitude = "latitudeField"; // latitudeField is a field in your data
imageSeries.mapImages.template.propertyFields.longitude = "longitudeField"; // longitudeField is a field in your data


import React from 'react';
import { Uppy } from '@uppy/core';
import { Dashboard } from '@uppy/react';
import GoldenRetriever from '@uppy/golden-retriever';


const App = () => {
  return (
    <div>
      <Dashboard uppy={uppy} plugins={['GoldenRetriever']} />
    </div>
  );
};


if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/golden-retriever-worker.js', {
    scope: '/',
  });
}


import React from 'react';
import Uppy from '@uppy/core';
import Tus from '@uppy/tus';
import { Dashboard } from '@uppy/react';

const FileUploader = () => {
  const uppy = new Uppy({
    restrictions: {
      allowedFileTypes: ['.jpg', '.jpeg', '.png'],
      maxFileSize: 5242880, // 5MB
      maxNumberOfFiles: 5
    },
    autoProceed: false
  });

  uppy.use(Tus, { endpoint: 'https://your-tus-server.com/files/' });

  uppy.on('complete', (result) => {
    console.log('Upload complete:', result.successful);
  });

  return (
    <div>
      <Dashboard
        uppy={uppy}
        plugins={['DragDrop']}
        proudlyDisplayPoweredByUppy={false}
      />
    </div>
  );
};

export default FileUploader;




e upload using ContextAPI and tus-js.

import Uppy from '@uppy/core'
import Tus from '@uppy/tus'

const uppy = new Uppy()
uppy.use(Tus, {
  endpoint: '=', // use your tus endpoint here
  resume: true,
  retryDelays: [0, 1000, 3000, 5000],
}





Ashwini CM
How to send file using contextapi and reducer using tus-js-client

To send a file using Context API and Reducer using tus-js-client, you can follow these steps:

Install tus-js-client package:
Copy code
npm install tus-js-client
Create a Context and Reducer for your file uploading state:
javascript
Copy code
import React, { createContext, useReducer } from "react";

const initialState = {
  file: null,
  isUploading: false,
  progress: 0,
  error: null,
};

const reducer = (state, action) => {
  switch (action.type) {
    case "SET_FILE":
      return { ...state, file: action.payload };
    case "SET_UPLOADING":
      return { ...state, isUploading: action.payload };
    case "SET_PROGRESS":
      return { ...state, progress: action.payload };
    case "SET_ERROR":
      return { ...state, error: action.payload };
    default:
      return state;
  }
};

export const UploadContext = createContext();

export const UploadProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <UploadContext.Provider value={{ state, dispatch }}>
      {children}
    </UploadContext.Provider>
  );
};
Create a component to handle the file upload:
javascript
Copy code
import React, { useContext } from "react";
import tus from "tus-js-client";
import { UploadContext } from "./UploadContext";

const FileUploader = () => {
  const { state, dispatch } = useContext(UploadContext);

  const handleFileChange = (event) => {
    const file = event.target.files[0];
    dispatch({ type: "SET_FILE", payload: file });
  };

  const handleUpload = () => {
    const file = state.file;
    if (!file) {
      dispatch({ type: "SET_ERROR", payload: "No file selected" });
      return;
    }

    const upload = new tus.Upload(file, {
      endpoint: "http://example.com/files/",
      chunkSize: 5242880,
      retryDelays: [0, 3000, 5000, 10000, 20000],
      metadata: {
        filename: file.name,
        filetype: file.type,
      },
      onError: (error) => {
        dispatch({ type: "SET_ERROR", payload: error });
      },
      onProgress: (bytesUploaded, bytesTotal) => {
        const progress = (bytesUploaded / bytesTotal) * 100;
        dispatch({ type: "SET_PROGRESS", payload: progress });
      },
      onSuccess: () => {
        dispatch({ type: "SET_UPLOADING", payload: false });
      },
    });

    upload.start();
    dispatch({ type: "SET_UPLOADING", payload: true });
  };

  return (
    <div>
      <input type="file" onChange={handleFileChange} />
      <button onClick={handleUpload}>Upload</button>
      {state.isUploading && <div>Uploading... {state.progress}%</div>}
      {state.error && <div>Error: {state.error.message}</div>}
    </div>
  );
};

export default FileUploader;
Wrap your component with the UploadProvider:
javascript
Copy code
import React from "react";
import FileUploader from "./FileUploader";
import { UploadProvider } from "./UploadContext";

const App = () => {
  return (
    <UploadProvider>
      <FileUploader />
    </UploadProvider>
  );
};

export default App


Open sidebar
React ContextAPI with Reducer - File Upload


Ashwini CM
Using contextapi reducer how to send file in react

The Context API in React is a way to share data between components without passing the data through props. A reducer is a function that takes in a state and an action, and returns a new state based on the action.

To send a file using the Context API with a reducer in React, you can follow these steps:

Define an initial state with an empty file object in your reducer function. For example:
php
Copy code
const initialState = {
  file: null
};

function reducer(state, action) {
  switch (action.type) {
    case "SET_FILE":
      return { ...state, file: action.payload };
    default:
      return state;
  }
}
Create a new context using the createContext function and pass in the initialState and the reducer. For example:
javascript
Copy code
export const FileContext = createContext(initialState);

export const FileProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <FileContext.Provider value={{ state, dispatch }}>
      {children}
    </FileContext.Provider>
  );
};
Create a file input in your component and set an onChange event that dispatches a SET_FILE action to the reducer. For example:
javascript
Copy code
import { useContext } from "react";
import { FileContext } from "./FileContext";

function FileUploader() {
  const { dispatch } = useContext(FileContext);

  const handleFileUpload = (event) => {
    dispatch({ type: "SET_FILE", payload: event.target.files[0] });
  };

  return (
    <div>
      <input type="file" onChange={handleFileUpload} />
    </div>
  );
}

export default FileUploader;
Access the file object in any component that needs it by using the useContext hook and passing in the FileContext. For example:
javascript
Copy code
import { useContext } from "react";
import { FileContext } from "./FileContext";

function FilePreview() {
  const { state } = useContext(FileContext);

  return (
    <div>
      {state.file && (
        <img src={URL.createObjectURL(state.file)} alt="file preview" />
      )}
    </div>
  );
}

export default FilePreview;
In this example, the FilePreview component displays the file that was uploaded in the FileUploader component by accessing the file object in the state object of the FileContext.

Note: When sending a file to a server, you would typically need to use additional APIs or libraries such as FormData or axios to actually upload the file. The above code only demonstrates how to use the Context API and reducer to manage the state of a file object in your React application.





Send a message.


Free Research Preview. ChatGPT may produce inaccurate information about people, places, or facts. ChatGPT Mar 23 Version
New chat

This code creates a Context and Reducer for your file uploading state, and a component to handle the file upload using tus-js-client. When a file is selected and the "Upload" button




Open sidebar
New chat


User
Pause and resume button not working in tus-js-client between pages please provide complete full react code,

3 / 3


ChatGPT
To help you with this issue, I'll provide a sample React code that demonstrates how to implement the tus-js-client library to handle file uploads with a pause and resume feature. Here's the code:

javascript
Copy code
import React, { useState } from "react";
import tus from "tus-js-client";

const Upload = () => {
  const [file, setFile] = useState(null);
  const [upload, setUpload] = useState(null);
  const [isUploading, setIsUploading] = useState(false);
  const [progress, setProgress] = useState(0);

  const handleFileChange = (e) => {
    setFile(e.target.files[0]);
  };

  const handleUpload = () => {
    setIsUploading(true);

    const upload = new tus.Upload(file, {
      endpoint: "http://your-tus-server.com/files/",
      resume: true,
      chunkSize: 5 * 1024 * 1024, // 5MB chunks
      retryDelays: [0, 1000, 3000, 5000],
      metadata: {
        filename: file.name,
        filetype: file.type,
      },
      onError: (error) => {
        console.log("Upload failed:", error);
        setIsUploading(false);
      },
      onProgress: (bytesUploaded, bytesTotal) => {
        const progress = (bytesUploaded / bytesTotal) * 100;
        setProgress(progress);
      },
      onSuccess: () => {
        console.log("Upload complete!");
        setIsUploading(false);
      },
    });

    setUpload(upload);
    upload.start();
  };

  const handlePause = () => {
    upload.abort();
    setIsUploading(false);
  };

  const handleResume = () => {
    setIsUploading(true);
    upload.start();
  };

  return (
    <div>
      <input type="file" onChange={handleFileChange} />
      <button onClick={handleUpload} disabled={!file || isUploading}>
        Upload
      </button>
      {isUploading && (
        <>
          <button onClick={handlePause}>Pause</button>
          <button onClick={handleResume}>Resume</button>
        </>
      )}
      <div>{progress}%</div>
    </div>
  );
};

export default Upload;
In this code, we define a Upload component that contains the state for the file to be uploaded, the tus-js-client Upload instance, whether the upload is currently in progress, and the progress percentage. The handleFileChange function updates the file state when a file is selected. The handleUpload function creates a new Upload instance with the specified options, sets the upload state to the new instance, and starts the upload. If the upload fails, the onError callback is called and the isUploading state is set to false. If the upload progresses, the onProgress callback is called and the progress state is updated. If the upload completes successfully, the onSuccess callback is called and the isUploading state is set to false.

The handlePause function aborts the current upload and sets the isUploading state to false. The handleResume function starts the upload again


Send a message.

···

Free Research Preview. ChatGPT may produce inaccurate information about people, places, or facts. ChatGPT Mar 23 Version


import React, { useState } from 'react';
import Uppy from '@uppy/core';
import Tus from '@uppy/tus';
import { DragDrop } from '@uppy/react';

const FileUploader = () => {
  const [progress, setProgress] = useState(0);
  const [isUploading, setIsUploading] = useState(false);
  const [uploadError, setUploadError] = useState(null);

  const uppy = Uppy({
    debug: true,
    autoProceed: false,
    restrictions: {
      maxFileSize: 10000000, // 10MB
    },
  }).use(Tus, { endpoint: 'https://your-tus-server.com/files' });

  uppy.on('upload-progress', (file, progress) => {
    setProgress(progress);
  });

  uppy.on('upload-success', (file) => {
    setIsUploading(false);
    console.log('Upload complete:', file);
  });

  uppy.on('upload-error', (file, error) => {
    setIsUploading(false);
    setUploadError(error);
  });

  const startUpload = () => {
    setIsUploading(true);
    uppy.upload();
  };

  const cancelUpload = () => {
    uppy.cancelAll();
    setIsUploading(false);
  };

  return (
    <div>
      <DragDrop uppy={uppy} />

      {isUploading && (
        <div>
          <progress value={progress} max="100"></progress>
          <button onClick={cancelUpload}>Cancel</button>
        </div>
      )}

      {uploadError && <p>Error: {uploadError}</p>}

      <button onClick={startUpload} disabled={isUploading}>
        Start Upload
      </button>
    </div>
  );
};

export default ;


import React, { useState } from 'react';
import Uppy from '@uppy/core';
import UppyDashboard from '@uppy/dashboard';
import UppyProgressBar from '@uppy/progressbar';
import '@uppy/core/dist/style.css';
import '@uppy/dashboard/dist/style.css';
import '@uppy/progressbar/dist/style.css';

const FileUploader = () => {
  const [progress, setProgress] = useState(0);

  const uppy = Uppy({
    debug: true,
    autoProceed: false,
    restrictions: {
      maxFileSize: 1000000, // 1MB in bytes
    },
  })
    .use(UppyDashboard, {
      target: '#uppy-dashboard',
      inline: true,
    })
    .use(UppyProgressBar, {
      target: '#uppy-progress-bar',
      hideAfterFinish: false,
    });

  uppy.on('upload-progress', (file, progress) => {
    setProgress(progress.percent);
  });

  const handleUpload = async () => {
    const result = await uppy.upload();
    console.log('Upload complete!', result.successful);
  };

  return (
    <div>
      <div id="uppy-dashboard"></div>
      <div id="uppy-progress-bar"></div>
      <progress value={progress} max="100"></progress>
      <button onClick={handleUpload}>Upload</button>
    </div>
  );
};

export default FileUploader;

Use
@uppy/react exposes c

import React, { useEffect } from 'react';
import Uppy from '@uppy/core';
import Webcam from '@uppy/webcam';
import { Dashboard } from '@uppy/react';

// Don't forget the CSS: core and the UI components + plugins you are using.
import '@uppy/core/dist/style.min.css';
import '@uppy/dashboard/dist/style.min.css';
import '@uppy/webcam/dist/style.min.css';

// Don’t forget to keep the Uppy instance outside of your component.
const uppy = new Uppy().use(Webcam);

function Component() {
    return <Dashboard uppy={uppy} plugins={['Webcam']} />;
}


const uppy = new Uppy().use(Webcam);

function Component(props) {
    useEffect(() => {
        uppy.setOptions({ restrictions: props.restrictions });
    }, [props.restrictions]);

    useEffect(() => {
        uppy.getPlugin('Webcam').setOptions({ modes: props.webcamModes });
    }, [props.webcamModes]);

    return <Dashboard uppy={uppy} plugins={['Webcam']} />;

NOTE
This is the only exception for having Uppy inside the component.

import { useState, useEffect } from 'react';
import { Uppy } from '@uppy/core';
import { DragDrop, StatusBar } from '@uppy/react';
import Transloadit from '@uppy/transloadit';

import '@uppy/core/dist/style.min.css';
import '@uppy/drag-drop/dist/style.min.css';
import '@uppy/status-bar/dist/style.min.css';

function createUppy(houseId, roomId) {
    // Adding to global `meta` will add it to every file.
    // Every Uppy instance needs a unique ID.
    return new Uppy({ id: roomId, meta: { houseId, roomId } }).use(Transloadit, {
        assemblyOptions(file) {
            return {
                params: {
                    auth: { key: 'TRANSLOADIT_AUTH_KEY_HERE' },
                    template_id: 'xyz',
                    // Send the results of the assembly to your backend.
                    notify_url: 'https://your-domain.com/assembly-status',
                },
                // You can use these inside your template
                // https://transloadit.com/docs/topics/assembly-instructions/#form-fields-in-instructions
                fields: { roomId: file.meta.roomId, houseId: file.meta.houseId },
            };
        },
    });
}

export default function Room(props) {
    const { houseId, roomId } = props;
    // important: passing a initializer function to prevent the state from recreating.
    const [uppy] = useState(() => createUppy(houseId, roomId));

    useEffect(() => {
        if (houseId && roomId) {
            uppy.setOptions({ meta: { houseId, roomId } });
        }
    }, [uppy, houseId, roomId]);

    return (
        <>
            <DragDrop uppy={uppy} />
            <StatusBar uppy={uppy} />
        </>
    );
}

