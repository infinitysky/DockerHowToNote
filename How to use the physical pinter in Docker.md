# How to use the `physical printer` in Docker?

When the Docker comes out and the printing task created by CUPs in a Docker container, then there is a question that I have to resolve.

## "How to print inside a docker container?"

Here is the solution:
do not install the CUPs inside the container, and Bind mount a volume into the container.

```
  -v /var/run/cups:/var/run/cups:ro -v /etc/cups:/etc/cups:ro -v /usr/lib/cups:/usr/lib/cups:ro -v /usr/share/cups:/usr/share/cups:ro -v /usr/bin/lp:/usr/bin/lp:ro

  ```


  for example:
I created an image, and I start run the image to container.
The CMD I am using is:
```
  sudo docker run -ti -v /var/run/cups:/var/run/cups:ro -v /etc/cups:/etc/cups:ro -v /usr/lib/cups:/usr/lib/cups:ro -v /usr/share/cups:/usr/share/cups:ro -v /usr/bin/lp:/usr/bin/lp:ro -p 23:22 -p 80:80 -p 8188:8188 -p 8189:8189 -p 3306:3306 -p 9100:9100 -p 8088:8088 --restart=always --name core81  coreserver81 /usr/bin/supervisord

  ```

  Yes, by using the `-v` command to mount all the CUPS files from the host, then I can connect the printers on the host, and operate them from the docker container.

  The idea is from the concept of Linux/Unix, which is "everything is a file".
