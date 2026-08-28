# Picture Flow mods: how to draw your own records, CDs and tapes

Egle's **Picture Flow** is the 3D cover view of the Library. Instead of plain covers it can show your albums as vinyl records, CD jewel cases, cassettes and cassette boxes, and you can decide which look goes on which album, artist, genre or era.

Everything you see there is drawn by Egle with vector shapes. A **mod** replaces one of those drawings with an image of your own: your photo of a real tape, a sleeve you painted, a label you designed. The album cover keeps working the way it does now, so a mod is a skin for the object, not for the artwork.

This page is the reference for people who make mods: the exact file for every part, the proportions it expects, where it has to be transparent, and what happens when you get it wrong.

Mods are a Supporter feature. If a Patreon tier lapses, the files stay on disk untouched, Egle just goes back to drawing the objects itself.

---

## Quick start

1. Open **Settings** and scroll to the **Picture Flow** section.
2. Find the **Graphic mods** row and click **New mod**. Give it a name, for example `Retro 80s`, and leave every layer ticked.
3. Egle creates the folder, fills it with **the standard artwork** as PNG files, and opens it for you.
4. Open the file you want to change in any image editor, paint over it, save it with the same name.
5. Go back to the Library, switch to Picture Flow and look at it. If Egle was already open while you edited, press **Refresh** in the same row.

That is the whole loop. You never start from a blank canvas and you never have to guess a file name.

**You can also do all of this without leaving the flow.** The **Manage views** window, the one you open from the Picture Flow itself, has a **General** tab holding the same mod panel: the source per object, the opacity sliders, upload, open folder and refresh. Change a mod there and the flow behind the window repaints straight away, so you can compare while you work. Settings keeps the same panel, and the two are the same thing, not two copies.

**Prefer to upload files one by one?** The **Upload** button next to each layer copies your image into the folder and renames it for you, so the name can never be wrong.

**Just want the artwork?** **Export standard artwork** writes all seventeen PNG files into any folder you pick, with no mod involved. You can also download them from this repository, in [`docs/picture-flow-mods-standard/`](picture-flow-mods-standard/).

---

## Where the files live

Mods live next to `egle_config.json`, inside a `skins` folder:

| Setup | Path |
|---|---|
| Normal install | `%APPDATA%\Egle\skins\` |
| Portable | the `skins` folder next to `egle.exe` |

Two ways to organize it:

```
skins\vinyl_disc.png            loose files, always active
skins\Retro 80s\vinyl_disc.png  the "Retro 80s" mod
skins\Chrome Tapes\cassette_shell.png
```

Loose files in `skins\` are the old, simple setup and they still work. A **mod folder** is just a subfolder with a name, and the selector in Settings switches between them.

An active mod **replaces** the loose files, it does not merge with them. If `Retro 80s` is selected, Egle only reads `skins\Retro 80s\`, so every layer has one clear source and the list in Settings tells the truth about what you are looking at.

### Taking one object from another mod

The mod you pick in the row is the **general source**, and it covers everything it has. On top of that you can send a single **object** to a different mod: the cassettes from one, the vinyl from another, without having to take a whole folder or leave it.

Open the layer list and you will see seven objects, each with its own source selector:

| Object | Files it covers |
|---|---|
| Vinyl record | `vinyl_disc` |
| Picture disc | `picture_disc` |
| Vinyl sleeve | `vinyl_sleeve` plus its two edges |
| CD case | `cd_case` plus its two edges |
| CD disc | `cd_disc` |
| Cassette | `cassette_shell`, `cassette_tape`, `cassette_hub` plus its two edges |
| Cassette case | `norelco_case` plus its two edges |

The grain is the object and not the single file on purpose: **the edges always travel with their own front**. A front from one mod with the edges of another is the one combination that should not be possible, because the two would never meet at the corner.

Three things to know:

- **there is no fallback between mods.** If the mod you picked for the cassettes does not have the tape, the tape goes back to Egle's drawing. It is not fetched from the general source, which would put back exactly the mismatch the rule above prevents;
- every mod in the selector shows **how much of that object it covers**, like `3 of 5`, so you can tell a cassette-only mod from a complete one before picking it;
- **an image you upload goes into the folder that row reads from.** What you see is what you edit, and the same goes for the bin: it removes the file from that mod, not from the general one.

Leave every object on **General source** and nothing changes: it is the old behaviour, one folder for the lot. There is also a **No mod** entry, which sends that one object to the loose files in `skins` and, if you have none, straight back to Egle's drawing.

Folder names can be up to 48 characters and cannot contain `\ / : * ? " < > |` or end with a dot. Everything else is fine, spaces included.

**Sharing a mod** is zipping its folder and sending it. The person who receives it drops the folder inside their own `skins\` and picks it from the selector. There is no manifest file, no version number, nothing to install.

If you copy files in by hand while Egle is open, press **Refresh** in the same row. Nothing watches the folder in the background.

---

## Rules that apply to every layer

- **PNG or WebP.** Nothing else is read, and the file picker will not even offer you anything else. A photo you found online is almost certainly a JPEG, so convert it first: any editor does it with Save as, and you want PNG anyway because most layers need transparency and JPEG has none.
- **8 MB per file, hard limit.** A file over the limit is ignored without a message and the skin goes back to its own drawing. If a layer you just filled looks unchanged, check the file size first.
- **PNG wins.** If both `vinyl_disc.png` and `vinyl_disc.webp` are in the folder, the PNG is used.
- **One file per layer.** There is no way to stack two images on the same part.
- **The image is stretched onto the object**, so the proportions in the tables below are the real millimetres of the real thing. A file with different proportions is still accepted, it just gets squashed, and Egle warns you when you upload it.
- **Size**: at least 256 px on the long side, or it looks soft in fullscreen. The standard files ship at 273 to 1000 px on the long side, except the two sleeve edges, which are narrow strips about 2100 px tall. Keeping the size of the standard file is the easy way to be right. Bigger files do not make the view slower, they only use memory.
- **Transparency matters for the layers that sit on top of the cover.** Those are marked in the tables. A fully opaque image there hides the album art completely.
- **Those same layers have an opacity slider** in their row, which saves you a round trip through the editor. See below.

### The opacity slider

The six layers that sit **on top of the cover** (`vinyl_disc`, `picture_disc`, `vinyl_sleeve`, `cd_case`, `cd_disc`, `norelco_case`) have a small slider in their row, next to the format badge. It appears as soon as the layer has an image.

Those layers work as a veil over the album art: grooves, plastic, sleeve texture, printing. How strong that veil should be is something you only find out by looking at the flow, and getting it right used to mean going back to the editor, changing the alpha, exporting, importing, looking again. The slider does it in place.

- **It is applied to the image, not to the view.** Egle multiplies the alpha channel when it loads the file, so nothing about the 3D, the reflection or the speed of the view changes.
- **Your file is not modified.** The slider is a setting, the PNG on disk stays exactly as you painted it, and putting it back to 100% gives you the original.
- **It only exists on those six.** On a cassette shell or an edge the image is the object itself, so lowering its alpha would not veil it, it would make a hole in it. Those rows have no slider.
- It travels with your settings, so it is in the backup zip like everything else.

A practical range: photographs of real materials usually land somewhere between 15% and 30% before the album art reads properly again. Start at 100%, look at the flow, come back and pull it down.

### What Egle keeps drawing, whatever you upload

This is the part that saves you work:

- **the album cover**, always;
- **the three openings of a cassette shell**, punched through your image, so the reels and the tape show through even if your photo is completely opaque;
- **the centre hole of a CD**, punched the same way;
- **the round shape** of vinyl faces, of the tape pack and of the reel hub, and the **rounded corners** of a cassette shell, so those images do not need transparent corners;
- **the tape motion, the spinning, the object sliding out of its case, the reflection and the 3D sides.**

A mod changes how a surface looks. It does not change how the object behaves.

### The standard artwork is the real drawing

The PNG files Egle gives you are not sketches or templates. They are photographs of what the app actually paints, taken from the running app with the album cover made invisible, so the transparency is already in the right places. Install all seventeen without touching them and the Picture Flow looks exactly as it did before.

Two consequences worth knowing:

- if you only want to change one detail, painting over the standard file is the safest route, because everything else stays pixel perfect;
- if a future version of Egle changes a drawing, your file keeps the old look. That is the point of a mod, but it is also why a layer can start looking out of place after an update. Export the artwork again to see what changed.

---

## The seventeen layers

### Vinyl family

| File | Used by | Proportions | Sits |
|---|---|---|---|
| `vinyl_disc` | Vinyl, Vinyl in sleeve | square | on top of the cover |
| `picture_disc` | Picture disc, in sleeve | square | on top of the cover |
| `vinyl_sleeve` | all three "in sleeve" entries | square (314 x 314 mm) | on top of the cover |
| `vinyl_sleeve_side_l` | the sleeve spine | 5.2 x 314 | edge, see below |
| `vinyl_sleeve_side_r` | the sleeve opening | 3 x 314 | edge, see below |

#### `vinyl_disc` (square, on top of the cover)

The black record, used both on its own and inside the sleeve.

- The image fills the whole square and **Egle does not round it**, so the corners must be transparent or you get a spinning square.
- **The label hole is a centred circle, 56.6% of the image width** (28.3% radius). The album cover is printed into that circle, so leave it transparent.
- The record spins while the album plays, so keep the drawing centred. Anything off centre will wobble.

#### `picture_disc` (square, on top of the cover)

This one is different from the others: **the image is only the marks**, the print is the album cover.

- The cover fills the whole face, then your image goes over it: grooves, the sheen sweep, the rim.
- So the image has to be **transparent almost everywhere**. If you paint a full disc here, you will not see any album art at all.
- Egle rounds it, so the corners do not matter.
- This is the layer to use if you want your records to carry the album art with your own grooves and gloss on top.

#### `vinyl_sleeve` (square, 314 x 314 mm, on top of the cover)

The cardboard sleeve, shared by the three "in sleeve" entries.

- The cover is printed on the **front panel, the left 99% of the width** (311 of 314). The thin strip on the right is the mouth the record slides out of.
- Your image goes over that, so leave the front panel transparent where you want the album art to show, and paint what real cardboard has: grain, ring wear, the fold, the cut edges, the shadow near the opening.
- You can also paint over the album art on purpose, for example a worn corner or a price sticker. That is what the "on top" order is for.

---

### CD family

| File | Used by | Proportions | Sits |
|---|---|---|---|
| `cd_case` | CD | 142 x 125 | on top of the cover |
| `cd_disc` | the disc that slides out | square | on top of the cover |
| `cd_case_side_l` | the case spine | 7.7 x 125 | edge, see below |
| `cd_case_side_r` | the opening edge | 7.7 x 125 | edge, see below |

#### `cd_case` (142 x 125, on top of the cover)

The jewel case, front view, exactly the proportions of a real one lying wide.

- **The booklet window is x 10% to 98.6%, y 1.6% to 98.4%.** That rectangle has to be transparent, it is where the cover shows.
- The left 10% is the **spine**, the black ribbed strip. That is where a case reads as a case, so it is worth drawing properly.
- Paint the glass: the frame, the highlights, the edge. It sits over the artwork, so reflections on top of the cover look right.

#### `cd_disc` (square, on top of the cover)

The disc that slides out of the case while the album plays.

- The cover is printed in a circle that reaches **99% of the disc radius**, then your image goes over it.
- **The centre hole is punched by Egle** at 12.5% of the radius, so you do not need to cut it.
- Leave the print ring transparent, **from 27% to 99% of the radius**, or the album art disappears.
- Inside 27% of the radius is the **clamping ring and the hub**, the clear plastic part that is never printed. Your image is what draws it.
- The disc spins, so keep it centred and touching the edges of the square.

---

### Cassette family

| File | Used by | Proportions | Sits |
|---|---|---|---|
| `cassette_shell` | Cassette, standard model | 100.4 x 63.8 | under the cover |
| `cassette_tape` | the wound tape, every model and pose | square | inside, seen through the openings |
| `cassette_hub` | the reel hub, every model | square | inside, seen through the openings |
| `cassette_side_l` / `_r` | Cassette, lying and standing | 9 x 63.8 | edge, see below |
| `norelco_case` | Cassette in case, both poses | 69.6 x 109 | on top of the cover |
| `norelco_side_l` / `_r` | the case spine and opening edge | 12.9 x 109 | edge, see below |

#### `cassette_shell` (100.4 x 63.8, under the cover)

The shell of the **standard** cassette model. The Type IV and the white shell keep Egle's own drawing, on purpose: their label area, recess and openings sit in different places, so one photo could not line up with all three. If you want your own cassette, pick the standard model in the skin selector.

This is the friendliest layer to mod:

- **your image can be completely opaque.** Egle punches the openings through it and prints the cover on top, so a straight photo of a tape works.
- **corners are rounded for you.**
- The label rectangle, where the album cover gets printed, is `x 8%, y 4.7%, 84.1% x 70.5%` of the image.

So: photograph or draw the shell **without a label**, and leave the label area plain. Egle stamps the album art there.

#### `cassette_tape` (square) and `cassette_hub` (square)

What you see through the three openings. These two are shared by every cassette model and by both poses, and they also show inside the case once the tape slides out.

- `cassette_tape` is the **full tape pack**, the disc of wound tape at its widest. Draw it filling the square, edge to edge. As the track plays, Egle **crops** your image to the current radius instead of scaling it, exactly like a real tape unwinding: you see the inner part of your own texture, and the winding lines keep their size.
- `cassette_hub` is the **hub**, the plastic core with its toothed hole. It is small on screen (about 25 px in a window, about 60 px in fullscreen) but it is the internal part you see the most, since the two round windows are cut around it. Draw the teeth and the hole, that is what makes it read as a hub.
- Both are cut into a circle for you, so the corners can be anything and a photo works.

#### `norelco_case` (69.6 x 109, on top of the cover)

The clear plastic box.

- **One file for both poses.** Draw it standing up, in the proportions above. When the case is lying down Egle rotates the same image 90 degrees, which puts the spine where that pose needs it.
- The J-card print window is **x 1.6% to 97.3%, y 3.4% to 96.6%**. Leave it transparent, that is where the cover shows.
- Everything else is the plastic: the frame, the spine, the little valve teeth, the highlights.

---

### The eight edges (the 3D thickness)

`vinyl_sleeve_side_l/r`, `cd_case_side_l/r`, `cassette_side_l/r`, `norelco_side_l/r`.

Every package in the Picture Flow has real thickness: two faces turned 90 degrees that fall back behind the front. Those faces are what you are painting here.

- `_l` and `_r` mean **the left and the right side as you see them in the flow**, not two named parts of the object. An object with two poses uses the same file in both.
- **They only show on the side covers.** The cover in the middle faces you straight on, so its edges are invisible by construction. Turn your head to the covers left and right of it and you see them clearly: about 30 px for the cassette case and 15 px for the bare cassette on a 193 px cover, twice that in fullscreen.
- **They disappear if 3D thickness is off.** That is a switch in Settings, and some people turn it off for performance. Your edge images go with it.
- They are **narrow, tall strips**. The sleeve opening is 3 mm on a 314 mm sleeve, so its file is about 20 px wide and 2000 px tall. That is not a mistake, it is the shape of the real thing. Scale it up in your editor if you want room to paint, then save it back at any size with the same proportions.
- The reflection under the object is painted for you from the same image, so you do not have to draw it.

---

## Warnings and errors

When you upload through Settings, Egle reads the image and tells you what it found. **Warnings never block the upload**, the file is installed anyway:

| Warning | What it means |
|---|---|
| Proportions differ from the expected ones | more than 2% off, the image will be stretched. Sometimes that is what you want |
| No transparency | the image is fully opaque on a layer that sits on top of the cover, so the album art will be hidden. This is the classic result of exporting without deleting the background |
| Image is small | under 256 px on the long side, it will look soft in fullscreen |

These do block it:

| Error | Fix |
|---|---|
| Unsupported format | use PNG or WebP |
| File too large | keep it under 8 MB |
| Unreadable image | the file is corrupted or is not really an image |

A file over 8 MB copied in **by hand** is a special case: it is skipped silently, with no message anywhere, and the layer keeps showing Egle's own drawing. That is deliberate for a folder you fill yourself, but it is the first thing to check when a layer refuses to change.

---

## Checklist before you export

- Right proportions for the layer.
- Transparent where the cover has to show, if the layer sits on top of it.
- No label drawn on the cassette shell, Egle prints one.
- Centre your artwork on the layers that spin (`vinyl_disc`, `picture_disc`, `cd_disc`, `cassette_tape`, `cassette_hub`).
- 800 px or more on the long side, under 8 MB.
- PNG unless you have a reason to use WebP.
- Paint the veil layers at full strength and pull them back with the slider in Settings, instead of baking a low alpha into the file.

---

## Troubleshooting

**I uploaded an image and nothing changed.** Check that the right mod is selected in the row, then press Refresh. If you copied the file by hand, check the name against the tables and check the size against the 8 MB limit.

**The album cover disappeared.** The layer sits on top of the cover and your image has no transparency where the cover is meant to show. Look up the window in this page.

**My cassette shows two labels.** You drew one on the shell. Leave the label area plain, Egle prints the album art there.

**My cassette shell image does nothing.** You are looking at the Type IV or the white model, which are always drawn by Egle. Pick the standard model in the skin selector.

**The record has square corners.** Only `vinyl_disc` needs transparent corners, the other round layers are cut for you.

**I painted an edge and cannot see it.** Edges only show on the side covers, never on the one in the middle, and they are hidden entirely when 3D thickness is switched off in Settings.

**I picked a mod for one object and half of it went back to Egle's drawing.** That mod does not have those files. There is no fallback between mods, on purpose. The count next to its name in the selector tells you how many of that object's files it has.

**I uploaded a file and it landed in the wrong mod.** The upload goes into the folder that row reads from, which is the object's source and not necessarily the general one. Check the selector on that object's header before uploading.

**The opacity slider is missing on a layer.** Either the layer has no image yet, or it is one of the eleven that do not sit on top of the cover, where opacity would make a hole instead of a veil.

**Everything went back to the default drawings.** Mods are a Supporter feature. Your files are still on disk and come back as soon as the tier is active again.

---

Made something good? The Picture Flow is the part of Egle people screenshot, so feel free to share your mod folder on the [Patreon](https://www.patreon.com/cw/egleMusic) page.
