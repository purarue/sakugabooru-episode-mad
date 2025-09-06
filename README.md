# sakugabooru-episode-mad

Downloads all [sakugabooru](https://www.sakugabooru.com/) posts for a particular tag, and optionally lets you combine them into Source(episode)-based videos using ffmpeg

## Installation

Requires `python3.9+`

To install with pip, run:

```
pip install git+https://github.com/purarue/sakugabooru-episode-mad
```

## Usage

```
Usage: python -m sakugabooru_episode_mad download [OPTIONS] TAG

  Download posts from Sakugabooru

Options:
  --download / --skip-download    download media, or just grab medata from
                                  each post
  -S, --skip-score-under INTEGER  skip posts with score under this value
  -o, --output-folder TEXT        output folder
  --only-animated / --all         only download animated posts, or all posts
  --help                          Show this message and exit.
```

`sakugabooru_episode_mad download <tag name>` to download all posts with that tag

Once that's done, you can `merge` them into a video using the `Source` metadata from each post. Typically, that is an episode, but if its from a movie/OP/ED, it'll just be marked as `Episode 0`

```
Usage: python -m sakugabooru_episode_mad process [OPTIONS] FOLDER

  Process/List downloaded posts

Options:
  -s, --sort-by TEXT
  -o, --output-type [json|media_path|id|url|file_url|merge_videos]
  -g, --group-by [source]         group by source, or not when merging into
                                  combined video
  --reverse / --no-reverse        reverse sort order
  --help                          Show this message and exit.
```

There are some `--output-type`s to just view the data from the JSON files, otherwise if you want to merge the downloaded videos, use something like:

```
sakugabooru_episode_mad process --output-type merge_videos --group-by source <folder>
```

## Examples

- `sakugabooru_episode_mad download flanders_no_inu -S 25`
- `sakugabooru_episode_mad download 'shoujo_kakumei_utena' --only-animated --download`
- `sakugabooru_episode_mad download the_super_dimension_fortress_macross`

Downloading and `ffmpeg`ing into a single file:

```bash
sakugabooru_episode_mad download one_piece --only-animated --skip-score-under 100
sakugabooru_episode_mad process one_piece -o merge_videos -g source
```
