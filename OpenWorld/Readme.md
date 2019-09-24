/* OPEN_WORLD_README

This package was developed and created by CloseRange.

To use this package start off by creating a main generation object. 
For this example I'll call it obj_generate.
IMPORTANT: this object should be marked as persistant
in the create event for obj_generate call the script:
openWorldInit(forceReset, focusObject, chunkSize, [padding]);
    1. Force Reset
        this should be true or false. true when you are developing and false when it's ready for release
        each 'room' or 'chunk' is saved to a ini file at the start of the game.
        setting this to true means that it will remake each file even if the files already exist
    2. Focus Object
        this is a single object that will ALWAYS be at the center of the view.
        this could be the player or a seperate object that follows the player.
        You may move it as you will but note that there should only be 1 of these objects ever. NOT 1 in every room, but 1 of them anywhere
    3. Chunk Size
        this is important. chunk size is how big each room will be.
        each room acts as a chunk of the overall world, so it's important that each room or 'chunk' stays the same size.
    4. padding (optional)
        by default padding is .2
        padding defines how far into the next chunk you need to be before it loads the next set of chunks.
        if this was set to 0 and you stood at the edge of a chunk and walked back and forth, you'd constantly be loading and unloading chunks.
        padding helps to reduce how often you need to unload /reload chunks.
        
under that script you can start adding new chunks to the world by using the script:
openWorldRoom(chunkX, chunkY, room);
    1. 2. Chunk X, Chunk Y
        this is where the  chunk is located in the world.
        for example 0, 0 is the top left chunk
        1, 0 is the chunk directly to the right of that
        0, 1 is the chunk directly below it
    3. Room
        this is what room to use as the chunk.
        objects and tiles outisde the room bounds will still be generated so be careful
        views in these rooms will not be affected
        instance create codes and room create codes will not be affected
        
in some cases you will have objects that need to save their current state.
for instance a chest that needs to stay open.
Normally, because objects are deleted then recreated when you walk too far away, all variables will return to normal.
For objects like this you should call a script on them, right under where you initalize the chunks using the script:
nonStatic(object);

on the off chance that you only need some instances to be static and some to not be
like if only some chests need to be non static
give the object a variable called STATIC and set it equal to false.
by default STATIC is true.

example use:
----------------------------
openWorldInit(true, obj_player, 640);

openWorldRoom(0, 0, room0);
openWorldRoom(1, 0, room1);
openWorldRoom(0, 1, room2);
openWorldRoom(1, 1, room0);
----------------------------

finally, in the step event for obj_generate add the script:
openWorldStep();

----------------------------

now that the object has been create you can add the main world room.
Create an empty room, the name and room size doesn't matter at all.
the ONLY object that should be present is obj_generate

make sure to show and enable use of views.
The view size should be NO BIGGER than 2 times the chunk size.
so if the chunk size is 640 then the biggest the view should be is 1280

    
*/

