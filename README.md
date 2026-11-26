# SSP Labels website

One-page site for Shivay Screen Printer (SSP Labels), Ludhiana.

## Deploy
Upload this folder to Netlify as it is. `index.html` loads every picture from `images/`, so keep the two together.

## Images
Each picture on the page is a named slot. To replace one, save a new file with the same name in `images/` (`.webp`, `.png` or `.jpg`). While an image loads, or if it's missing, the page shows a light placeholder of the same shape.

- `docs/SSP_image_prompts_and_placement.md`: every slot, its file name, size and where it appears
- `docs/SSP_gemini_prompts_ready_to_paste.md`: Gemini prompts for the product, photo and machine slots
- `docs/SSP_more_image_ideas.md`: prompts for the process, finishes, industry and label-roll images

Still to generate: `finish_spotuv`, `ind_food`, `rolls_stack`, `rolls_cut`.
