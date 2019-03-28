# Chapter 05 - Building Images








<!-- ## Optimizing the Dockerfile

Note that the order of the instructions does play a significant role when creating a `Dockerfile`. During the process of building an image Docker steps through the instructions in your `Dockerfile `executing each in the order specified. As each instruction is examined, Docker looks for an previous generated intermediate image in its cache that it can reuse, rather than creating a new \(duplicate\) image. This means that your build stage layers \(created by most `Dockerfile `instructions\) should be ordered from the less frequently changed to the more frequently changed allowing maximum use of cached images, and speeding up building times immensely. -->

<!-- So we should refactor the dockerfile a bit to optimize it. -->

## Common Dockerfile Instructions

The table below lists the most common used instructions for a Dockerfile.

| Instruction | Details |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `FROM` | When creating a Dockerfile it should always specify **on which image it should be based**. This is achieved using the `FROM` instruction. A common source of images to base your image on is Docker Hub. Specify a specific tag using a colon `:<version_number>`use the latest image using `:latest` |
| `WORKDIR` | Sets the **working directory** for instructions that follow. If the directory does not exist yet, it will be created. |
| `RUN` | Allows the **execution of commands in the shell**. This is for example used to install applications, libraries or other dependencies. Each `RUN` instruction will execute any commands in a new layer on top of the current image and commit the results |
| `ENV` | Sets an **environmental variable **to a specified value. These **will persist **when a container is running. Environment variable are used to inject variables in the container that can be used for any reason. eg: setting server settings, user accounts,.... |
| `COPY <src> <dst>` | **Copies files and directories** from the host file system to the image. Relative paths can be used for both the source and the destination. Relative paths in the destination are relative to the working directory. |
| `EXPOSE <port>/<udp,tcp>` | Indicates that the **container must open the specified ports** when running. If no protocol is specified, than it **defaults to tcp**. Do note that the `EXPOSE` instruction does not actually publish the port - this needs to be done when running the container. |
| `CMD ["executable","arg1","arg2"]` | Specifies the application or **executable process that needs to be run** in the container when started. Only a single CMD instruction can be specified within a Dockerfile. |