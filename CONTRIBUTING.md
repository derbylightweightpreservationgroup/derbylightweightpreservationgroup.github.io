# Editing the Derby Lightweight Preservation Group website

Most routine content can be maintained through Pages CMS. The CMS exposes Updates, The Train, Restoration, Support Us, About, Contact and Restoration Status. It does not expose site configuration, dependencies, templates or build files.

Pages CMS is an editing interface, not a substitute for GitHub repository permissions. Anyone with direct repository access may still be able to edit files outside the CMS.

## Before editing

- Replace only information that has been checked and approved for publication.
- Leave `[TO BE CONFIRMED: ...]` in place when a fact is not yet known or approved.
- Do not publish personal contact details, volunteer names or private working arrangements without permission.
- Preview the generated site or ask a maintainer to check it before publishing substantial changes.

## Writing updates

- Use a specific title and a short summary that makes sense on its own.
- Choose the closest category, vehicle and work area from the supplied lists.
- Use Heading 2 for sections within a page or update; the page title is already Heading 1.
- Link with descriptive words such as "read the restoration update", not "click here".
- The initial sample post and `assets/uploads/example-update.png` are demonstration content and must be deleted before launch.

## Preparing images

- Keep original high-resolution photographs and archival scans outside this website repository. Make a separate web copy rather than resizing or replacing the archival original.
- For ordinary website photographs, resize the web copy to approximately **2,000 pixels or less on the longest edge**.
- Aim for a file size below **1 MB** where this can be achieved without obvious loss of quality.
- Use JPEG for photographs, PNG for graphics that need crisp edges, or WebP for an efficient modern web image.
- Use short, descriptive, lowercase filenames with hyphens, for example `79018-cab-floor-repair.jpg`. Avoid spaces, dates without context and camera-generated names such as `DSC01234.JPG`.
- Write alternative text that conveys the image's useful content. Do not begin with "image of" and do not repeat the caption word for word.
- Add a caption when the date, place, people, vehicle, work or historical context would help a reader.
- Record the photographer or creator, source and copyright status wherever relevant. Confirm that the group has permission to publish the image before uploading it.

Pages CMS uploads web images to `assets/uploads/` and writes paths beginning `/assets/uploads/`. Each featured image in an update must have corresponding alternative text.

## Contact and corrections

Contact details and organisational facts remain placeholders until the group supplies approved wording. Search the repository for `TO BE CONFIRMED`, `CONTACT EMAIL` and `SAMPLE` before launch.
