# MCMap Build (Ubuntu OS based)

Pixel-art map visualizer for Minecraft. Maps are drawn from an isometric perspective.

---

### References

\- Main project source: <https://github.com/spoutn1k/mcmap>  
\- Docker image source: <https://github.com/serious-angel/docker-mcmap>  
\- Docker image: <https://hub.docker.com/r/artworks/mcmap>  

---

### Example

```bash
#!/usr/bin/env bash

# World Map Center Coordinates
x=-150; z=180;

radius=400;
from=( $(( x - radius )) $(( z - radius )) );
to=( $(( x + radius )) $(( z + radius )) );

mcmapOptions=(
    -file "/tmp/out/World.png"
    -from "${from[@]}"
    -to ${to[@]}
    -marker "$x" "$z" white
    '/tmp/World/'
);

docker run --rm -it \
    -v '/path/to/World/:/tmp/World:ro' \
    -v '/path/to/out:/tmp/out' \
    -- 'artworks/mcmap:latest' \
    "${mcmapOptions[@]}";
```

Once completed, the wonderful file should appear in:  
\- `/path/to/out/World.png`

At voilà! ✨

---

> Where you go matters less than who you are when you go.  
> ~ [Letters On Ethics To Lucilius](<https://archive.org/details/letters-on-ethics-to-lucilius-pdf-room/page/n125/mode/2up>) by Seneca [4BC-65AD]