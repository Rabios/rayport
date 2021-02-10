<div align="center">
    <img src="rayport.png" width="256", height="256">  
    <p>Awesome C99, Header-Only, <a href="https://github.com/SasLuca/rayfork">rayfork</a> wrapper for <a href="https://github.com/raysan5/raylib">raylib</a>!</p>
</div><br>

rayport wraps raylib API depending on what rayfork supports from raylib to keep compatibiltiy, Also RLGL and raymath wrapped!

You need to include `raylib.h` and rayfork to use rayport!

### Why rayport?

- Port raylib games easily to mobile and consoles via rayfork!
- Easy way to save porting time, You just need to rewrite window and input code (Depending on window and input library will used with rayfork).
- More independency to raylib code via rayfork (As rayfork can use any window and input library).
- rayport is written in C99, Making it portable and easy to use anywhere you name it!
- Can make bindings easier if you rely on rayfork but with using raylib!

### Example

Here is a simple example for rayport with rayfork uses `rayfork-sokol-template` (Include `rayport.h` with including rayfork and raylib previously!)

```c
#include "platform.h"
#include "raylib.h"
#include "rayport.h"

platform_window_details window = {
    .width  = 800,
    .height = 450,
    .title  = "rayfork"
};

rf_context ctx;
rf_render_batch batch;
Texture2D texture;

extern void game_init(rf_gfx_backend_data* gfx_data)
{
    // Initialize rayfork
    rf_init_context(&ctx);
    rf_init_gfx(window.width, window.height, gfx_data);

    // Initialize the rendering batch
    batch = rf_create_default_render_batch(RF_DEFAULT_ALLOCATOR);
    rf_set_active_render_batch(&batch);

    // Load texture
    texture = LoadTexture("bananya.png");
}

extern void game_update(const platform_input_state* input)
{
    // Render the image and clear the background to some nice shade of white
    BeginDrawing();
    ClearBackground(RAYWHITE);
    DrawRectangle(0, 0, 100, 100, RED);
    DrawTexture(texture, 0, 0, WHITE);
    EndDrawing();
}
```

Original code can be found [here](https://github.com/SasLuca/rayfork-tests/blob/master/special-setup-tests/simple-glfw/main.c).

### NOTES

1. Note that rayfork still miss some features unlike raylib, So some functions aren't wrapped yet!
2. Since 12/September/2020, You should include raylib easings header in order to use easings.
3. Although rayfork still miss some stuff, I successed lately in wrapping more stuff (And will still do)!
4. Don't use custom `rlgl.h` as RLGL since it's wrapped from `rayport.h`, That's to keep compatibility!
5. If you want to use custom `raylib.h` (Your own one), Make sure you add changes from the custom `raylib.h` i made.
6. If you don't care about step 5, I made a custom `raylib.h` ready for use with `rayport.h`, You just need to include it with rayfork.

> For list of available wrapped functions (As enums and colors wrapped), See [here](https://github.com/Rabios/rayport/blob/master/api.md).

> Also, See [changelog](https://github.com/Rabios/rayport/blob/master/changelog.md) for changes!

### Special Thanks

1. [Ramon Santamaria (raysan5)](https://github.com/raysan5), Who made [raylib](https://github.com/raysan5/raylib).
2. [Luca Sas (SasLuca)](https://github.com/SasLuca), Who made [rayfork](https://github.com/SasLuca/rayfork).
