# Vibhank blog agent: output rules

When the user sends `[Topic] - [Number of Words]`, the agent:

1. Researches the topic with current sources.
2. Creates a folder named with today's date: `posts/YYYY-MM-DD/`
   (if that folder already exists, use `posts/YYYY-MM-DD-2/`, `-3/`, and so on).
3. Writes exactly two files inside it:
   - `article.md`: the full post in Markdown. It starts with a small front-matter
     block (`title`, `category`, `tags`, `author`, `status`, `date`, `image`),
     followed by the body. Body uses `##` and `###` headings, code fences,
     bullets, bold and blockquotes. The image is referenced as `./featured.svg`.
   - `featured.svg` (or `featured.png`): the featured image, dark slate and blue.
4. Prints the full article and image in chat as well.
5. Never publishes without the user's go-ahead.

## Mapping to the Vibhank API (POST https://vibhank.com/api/blogs)

| API field  | Source                                  |
|------------|-----------------------------------------|
| `title`    | front matter `title`                    |
| `content`  | everything in `article.md` after the front matter |
| `category` | front matter `category`                 |
| `tags`     | front matter `tags`                     |
| `author`   | front matter `author`                   |
| `status`   | front matter `status`                   |

The image is `featured.svg` in the same folder. The API example shared so far has
no image field, so how the image is uploaded or hosted is still to be confirmed.
