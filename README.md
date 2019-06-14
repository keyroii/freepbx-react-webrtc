React.js component offering mobile and desktop browser voice and video communication. Wraps [sip.js](https://sipjs.com) with the nitty gritty details required make it work in such environments to help focus on application development.

To get started:

`$ npm install iotcomms-react-webrtc --save`

The component has been tested to work in combinations of the following web browsers updated to latest versions with video and voice calls:

* Safari on iOS
* Chrome on Android
* Safari on Mac
* Chrome on Mac
* Firefox on Mac

It is left as an exercise to the reader to check if it also works with the browsers above also on a Windows computer...

The main objective of the component is to provide a high-level logic providing WebRTC functionality to web applications where the developer should not have to dig into the details of how SIP, Peer connections, Sessions and Video elements interact during the lifecycle of a call.

It provides high level configuration through React.js Component properties. Once the component is mounted it will establish a connection back to the provisioned SIP server via WebSocket connection. From now it is ready to place and receive calls and it provides user interface to interact with the calls.

When the component is mounted it check that the application has been given permissions to use camera and microphone. If that is not the case information to the user is shown. It also informs if the browser is not supporting WebRTC, for example if it is started in a Chrome browser on an iPhone.

Below is an example of how to embed the component in a React.js application

```javascript

  import WebRTCClient from "iotcomms-react-webrtc";


  render() {
    return (
      <div className="App">
        //Video element used for rendering video self-view
        <video width="25%"  id="localVideo" autoPlay playsInline  muted="muted"></video>

        //Video element used for rendering video of remote party
        <video width="50%" id="remoteVideo" autoPlay playsInline ></video>

        <WebRTCClient
          video={true}
          autoRegister = {true}
          sipDomain={sipDomain}
          sipUser={sipUser}
          sipPassword={sipPassword}
          destination={destinationUri}
        />
      </div>
    );
  }
}

```

where

* The video elements must have the id's and attributes as provided in the example
* video property - indicates if video should be enabled for calls. If not, it will use voice only
* autoRegister property - indicates if the component should send a SIP Register to be able to receive calls
* sipDomain property - is the SIP domain to be used
* sipUser - is the user id to be used for authentication
* destination - is the remote destination to be called

When the component has mounted and have connection with the server a "Call" button is rendered. When this is pushed a call is placed to the destination configured in the destination property.

Upon incoming calls an "Answer" button is rendered.

The component will try to play out audio and video feedback when calling and alerting incoming calls. Due to autoplay limitations and logic in different web browsers this may not play.

*This project is sponsored by [iotcomms.io](https://iotcomms.io).*
