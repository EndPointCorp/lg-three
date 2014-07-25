lg-three.js
===========

Network view synchronization modification for THREE.js. 

To make this work, start with an existing THREE.js application.
* Include lg-three.js after including Three.js. Script should still work
  normally
* Also include socket.io, before lg-three
* Create slave HTML page that includes three.js, lg-three.js, socket.io, and
  the rendering container, and simply calls THREE.lg_init('appname', undefined,
  undefined, undefined, undefined, false);
    -- Note to self: Can we just create this automatically on the slave by
       interrogating the master?
* Create the initialScene function, to add all the meshes, etc. for the first
  rendering. It returns scene, camera, and renderer
    return { "scene" : scene, "camera" : camera, "renderer" : renderer };
* Have the master call THREE.lg_init('appname', preRenderMaster, preRenderSlave, initialScene, render, true);
* test -- should render something on the slave
* Modify preRender functions to capture anything that should update between
  renderings, and apply it on the slave
