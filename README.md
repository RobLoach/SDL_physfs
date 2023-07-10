# SDL_PhysFS

[PhysicsFS](https://github.com/icculus/physfs) is a portable flexible file I/O abstraction library. `SDL_PhysFS` builds upon [PhysFS's physfsrwops.h](https://github.com/icculus/physfs/blob/main/extras/physfsrwops.h) to ease the integration between SDL and PhysFS to load assets from *.zip* files.

## Example

``` c
#include <SDL2/SDL.h>

#define SDL_PHYSFS_IMPLEMENTATION
#include "SDL_PhysFS.h"

int main() {
    SDL_Init(SDL_INIT_EVERYTHING);

    // Initialize PhysFS
    SDL_PhysFS_Init();

    // Mount
    SDL_PhysFS_Mount("assets.zip", "assets");

    // Load a surface from assets.zip
    SDL_Surface* dog = SDL_PhysFS_LoadBMP("assets/dog.bmp");

    // Clean up
    SDL_PhysFS_Quit();
    SDL_Quit();

    return 0;
}
```

### API

``` c
SDL_bool SDL_PhysFS_Init();
SDL_bool SDL_PhysFS_InitEx(const char* org, const char* app);
SDL_bool SDL_PhysFS_Quit();
SDL_bool SDL_PhysFS_Mount(const char* newDir, const char* mountPoint);
SDL_bool SDL_PhysFS_MountFromMemory(const unsigned char *fileData, int dataSize, const char* newDir, const char* mountPoint);
SDL_bool SDL_PhysFS_Unmount(const char* oldDir);
SDL_RWops* SDL_PhysFS_RWFromFile(const char* filename);
SDL_Surface* SDL_PhysFS_LoadBMP(const char* filename);
SDL_AudioSpec* SDL_PhysFS_LoadWAV(const char* filename, SDL_AudioSpec * spec, Uint8 ** audio_buf, Uint32 * audio_len);
void* SDL_PhysFS_LoadFile(const char* filename, size_t *datasize);
size_t SDL_PhysFS_Write(const char* file, const void* buffer, size_t size);
SDL_bool SDL_PhysFS_SetWriteDir(const char* path);

// Optional Integrations
SDL_Surface* SDL_PhysFS_IMG_Load(const char* filename);    // SDL_image
Mix_Music* SDL_PhysFS_Mix_LoadMUS(const char* filename);   // SDL_mixer
SDL_Surface* SDL_PhysFS_STBIMG_Load(const char* filename); // SDL_stbimage.h
```

## License

[zlib](LICENSE)
