---
layout: post
title: Vim Is The Best
slug: vim-is-the-best
---

Recently I was working on a large JSON file similar to the one below. 
```
{
  "fog_devices": [
    .
    .
    .
    {
      .
      .
      .
      "neighbors": [
        "cloud_device_0",
        "edge_device_1",
        "phone",
        "camera",
        "car"
      ],
      .
      .
      .
    },
    .
    .
    .
}
```
Afterwards, I understood that I should have written `neighbors` as a list of dictionaries instead of a list of strings as shown below.
```
{
  "fog_devices": [
    .
    .
    .
    {
      .
      .
      .
      "neighbors": [
        { "neighbor_id": "cloud_device_0" },
        { "neighbor_id": "edge_device_1" },
        { "neighbor_id": "phone" },
        { "neighbor_id": "camera" },
        { "neighbor_id": "car" }
      ],
      .
      .
      .
    },
    .
    .
    .
}
```
I was not looking forward to manually changing each line. I knew that Vim macros would be the best way to go about this and 
I was using Vim plugin on IntelliJ IDEA. So here is what I did.

1. I opend the file and moved the cursor to the first line of the `neighbors` list.
2. I pressed `qa` to start recording a macro in register `a`.
3. I pressed `0` to move the cursor to the beginning of the line.
4. I pressed `f"` to move the cursor to the first `"` character.
5. I pressed `i{ "neighbor_id": ` to insert `{ "neighbor_id": ` at the beginning of the line.
6. I pressed `Esc` to exit insert mode.
7. I pressed `f"` twice to move the cursor to the second `"` character.
8. I pressed `a }` to insert ` }` at the end of the line.
9. I pressed `Esc` to exit insert mode.
10. I pressed `j` to move the cursor to the next line.
11. I pressed `q` to stop recording the macro.

Now I had a macro that would convert a line from the first format to the second format. I had to move the cursor to the each line of the `neighbors` list and run the macro by pressing `@a`.

All of this took me less than a minute. However, IntelliJ IDEA supports macros as well. 
So it may be possible to do the same thing without Vim, but why bother when Vim is the best and I can have it on all of my IDEs.