Imports
-------
#include <SDL2/SDL.h>
#include <SDL2/SDL_image.h>





Objects
-------

SDL_Window* w;
SDL_Surface* s;
SDL_Texture* t( std::string path );
SDL_Renderer* renderer;
    -needed for SDL_Textures
SDL_Event e;
    -e.type == SDL_QUIT, SDL_KEYDOWN, ...
    -SDL_KEYDOWN:
        -e.key.keysym.sym == SDLK_UP, SDLK_DOWN, SDLK_LEFT, SDLK_RIGHT


***Tips + Things to Do
enum KeyPresses {
    KEY_UP,
    KEY_DOWN,
    KEY_LEFT,
    KEY_RIGHT    
    NUM_KEYS_TOTAL
};

-Ensure all memory freed before exit (surfaces, windows, etc.)
    -set pointers to NULL when freed

-Init all pointer to NULL at declaration

int imgFlags = IMG_INIT_PNG;
if( !(IMG_Init(imgFlags) & imgFlags) )
    printf("%s", IMG_GetError() );
***



Texture Functions
-----------------
SDL_CreateTextureFromSurface( renderer, loadedSurface );
    -creates texture from surface

SDL_DestroyTexture( texture );
    -deallocates texture

SDL_RenderClear( renderer );
    -fills screen with last set SDL_SetRenderDrawColor( ... );

SDL_RenderCopy( renderer, texture, NULL, NULL );
    -renders texture to back buffer

SDL_RenderPresent( renderer );
    -updates screen for textures
    -cannot use SDL_UpdateWindowSurface with textures




Surface Functions
-----------------
SDL_FreeSurface( surface );
    -releases memory of surface

SDL_BlitSurface( source, NULL, destination, NULL );
    -copies source surface onto destination

SDL_BlitScaled( source, NULL, destination, %rect );
    -scales source surface to side of rect, blits onto destination

SDL_FillRect( surface, NULL, SDL_MapRGB(surface->format,0xFF,0xFF,0xFF));
    -fills Rectangle

SDL_LoadBMP("image/path/name.bmp");
    -loads bmp image, null if failed
    -takes a C string (std::string p  --> p.c_str())

IMG_Load("image/path/name.png");
    -same as LoadBMP except loads PNG, BMP, GIF, JPEG, etc...

SDL_ConvertSurface( loadedSurface, desiredSurface->format, NULL);
    -converts loaded surface to format of desiredSurface (surface of screen/window usually) for optimization





SDL Functions
-------------
SDL_Init( SDL_INIT_VIDEO ) 
    -returns -1 if error

SDL_GetError()
    -returns error as string

SDL_CreateWindow("Title",SDL_WINDOWPOS_UNDEFINED, SDL_WINDOWPOS UNDEFINED, width, height, SDL_WINDOW SHOW);
    -returns NULL if error

SDL_GetWindowSurface( window );
    -returns surface of window

SDL_UpdateWindowSurface( window );
    -updates surface of window

SDL_CreateRenderer( window, -1, SDL_RENDERER_ACCELERATED );
    -returns pointer to renderer for window

SDL_SetRenderDrawColor( renderer, 0xFF, 0xFF, 0xFF, 0xFF );
    -sets rendering color for renderer

SDL_Delay( x );
    -delays x milliseconds

SDL_DestroyWindow( window );
    -destroys window object

IMG_Quit();
    -quits IMG

SDL_Quit();
    -quits SDL

SDL_PollEvent( &e )
    -if no events in queue, returns 0
    -else, sets SDL_Event e as next event inline

SDL_Rect r;
    -r.x, r.y, r.w, r.h
