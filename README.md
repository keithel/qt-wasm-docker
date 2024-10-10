# Qt WebAssembly automated docker image generation

This is a small project showing how to automate the creation of a docker image
and docker-compose orchestration file in your Qt 6 project.

The reason to do this is so that your application is in a ready state to
distribute. Simply publish to docker hub, and give your users the docker hub URL
for your image.

The image can then run on clouds like AWS or GCP, locally on the user's machine,
or on some local servers.

The image uses alpine linux ensuring that the image size is minimal.

## make-docker-image

In this repository you will find a script called `make-docker-image`. This is
the main guts that does all the work. The rest I have to describe for you how to
use it, as it gets set up in the Qt Creator IDE, and stored in the
CMakeLists.txt.user file (so, something per-developer and not checked in
typically).

## Integrating into your Qt Wasm Project

First, put the `make-docker-image` script at the base of your Qt WebAssembly
project.

Next, to take use of this you will need to make some changes in your Qt project
under the WebAssembly "Build & Run" profile.

 * In the "Build Steps" section, create a "Custom Process Step".
 * Within this, in the `Command` field, put
   `%{CurrentDocument:Project:BuildConfig:Env:SHELL}`. You can find this
   yourself by pressing the A->B link at the end of the field, which will give
   you a list of properties and variables you can pick from. This is one of
   those.
 * For its `Arguments` (next field), use 
   `%{ActiveProject:Path}/make-docker-image %{ActiveProject:Name}`
 * Leave the `Working directory` field, leave it as the default of `%{buildDir}`

