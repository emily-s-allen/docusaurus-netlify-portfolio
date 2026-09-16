---
title: "SKILL.md, STYLEGUIDE.md, and Claude: My AI Documentation Experiment"
date: 2026-09-03
slug: skill-styleguide-and-claude
authors: yourname
tags: [ai-docs, claude, skill-file, style-guide, api-documentation, workflow, editorial-process]
hide_table_of_contents: true
---
I learn best by doing, and even better visually. I’ve done a lot of reading and research learning about AI Tech Writing workflows, but I hit the point where I wanted to see it with my own two eyes. So, inspired by seeing it across job descriptions, I set out to organize my own AI documentation workflow. And what better place to experiment than in my API docs portfolio. An endpoint document seems fairly straightforward. 

If you just want to see the files I used or the end result, those are linked here: 
- [SKILL.md](/files/SKILL.txt)
- [STYLEGUIDE.md](/files/STYLEGUIDE.txt)
- [The Final Draft](#the-final-draft)

If you’re interested in my process, my workflow and editorial decisions, and/or my commentary, stay here. 

## SKILL.md
From what I can tell, there’s not yet a standard way everyone is approaching AI tech writing – tools like Claude and Gemini are writing entire drafts, or AI built-in to documentation tools is supplementing content, or AI can provide reviews based on specific personas. My test will be to draft `SKILL.md` and `STYLEGUIDE.md` files, and then paste the raw data from Postman. This seems like a doable afternoon project. 

First, I did some research on skill files – how to structure them, what information to include, etc. With example files and some AI assistance from Claude to make sure I wasn’t missing anything crucial, I was able to whip up what looks like a halfway decent file. The thing that’s interesting about this file to me is that it is such a pure example of the importance of tech writing. It is basically very detailed instructions on completing a task and I know I’ve written similar content to train new hires and interns. 

Honestly (and maybe weirdly), I kind of love it. The way this file is organized is so similar to the way I think, especially about a task I’ve done a million times. I once took a medical leave and had to prep materials in advance, and so much of my prep was exactly like this. What are you doing; what needs to be included; what’s the step-by-step sequence; if it breaks, do this; etc.

## STYLEGUIDE.md
This one was, in some ways, a little more challenging for me, because my writing becomes automatic. I’m not thinking ‘use second-person, active voice’; I internalize the style and I write how I always write, which is according to a style guide that I’ve worked with forever. It’s like describing how to drive a car to someone who’s never driven – you use the gas, brake, steering wheel, mirrors, and signals without consciously thinking about it. Articulating and defining each step in an automatic behavior so a machine can perform the task was actually kind of uncomfortable, but genuinely useful in helping crystallize how the AI fits in a documentation workflow, and the importance of the skill and style guide files. 
  
I purposely kept the style guide fairly simple, defining voice and audience and sentence structure, and I may have some overlap with the skill file by mentioning all the sections that need to be in the document. I know one of the most important tenets for prompting AI is to provide examples and context for it to use, but I’m interested to see what the AI comes back with first, so I’ve purposely not included any examples. Spoiler: it did better than I thought it would.

## The First Draft
Skill and style guide files in hand, it’s time for the first draft. I created a new Claude project for a clean slate and briefly told it what I was looking for – write an API endpoint guide based on information I give you and instructions found in the `SKILL.md` and `STYLEGUIDE.md` files I uploaded to the project. Claude confirmed it found the files with a brief summary and prompted me for some information before it started. I provided it with the request URL, the optional and required parameters, and the real response body I had retrieved using Postman. It pretty quickly parsed through the information and returned this draft:

<details>

<summary>View the AI Draft</summary>

# Get Similar Movies

`GET` `https://api.themoviedb.org/3/movie/{movie_id}/similar`

Use this endpoint to get a list of movies similar to a given movie, based on shared genres and plot keywords. This is useful for building "you might also like" or recommendation sections in a movie app.

Because similarity is based on genres and keywords rather than deeper content analysis, results won't always be a perfect match. Treat this as a starting point for recommendations, not a precise similarity score.

## Prerequisites

This endpoint requires authentication. Include your API read access token as a bearer token in the request header (see **Request headers** below).

## Base URL

```
https://api.themoviedb.org/3
```

## Request headers

| Header | Required | Description |
|---|---|---|
| `Authorization` | Required | Your API read access token, formatted as `Bearer {token}`. |

## Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `movie_id` | integer | Required | The ID of the movie you want similar results for. |

## Query parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `language` | string | Optional | The language for the response, as an ISO 639-1 code. Defaults to `en-US`. |
| `page` | integer | Optional | The page of results to return. Defaults to `1`. |

## Example request

```
GET https://api.themoviedb.org/3/movie/533535/similar?language=en-US&page=1
Authorization: Bearer {your_token}
```

## Response fields

| Field | Type | Description |
|---|---|---|
| `page` | integer | The current page of results. |
| `results` | array | The list of movies similar to the requested movie. |
| `results[].adult` | boolean | Whether the movie is flagged as adult content. |
| `results[].backdrop_path` | string or null | The file path for the movie's backdrop image, relative to TMDB's image base URL. `null` if no backdrop is available. |
| `results[].genre_ids` | array of integers | The IDs of the genres associated with the movie. Match these against the `/genre/movie/list` endpoint to get genre names. |
| `results[].id` | integer | The unique TMDB ID for the movie. |
| `results[].original_language` | string | The original language of the movie, as an ISO 639-1 code. |
| `results[].original_title` | string | The movie's title in its original language. |
| `results[].overview` | string | A short plot summary of the movie. |
| `results[].popularity` | number | A relative popularity score TMDB calculates based on factors like votes, views, and watchlist adds. |
| `results[].poster_path` | string or null | The file path for the movie's poster image, relative to TMDB's image base URL. `null` if no poster is available. |
| `results[].release_date` | string | The movie's release date, in `YYYY-MM-DD` format. |
| `results[].softcore` | boolean | **Inferred, not in official documentation.** Appears to flag content of a softcore-adult nature, similar in purpose to `adult`. This field isn't listed in TMDB's published schema for this endpoint, so treat this definition as observed behavior rather than confirmed intent. |
| `results[].title` | string | The movie's title, localized to the requested `language`. |
| `results[].video` | boolean | Whether the entry has an associated video (for example, a direct-to-video release). |
| `results[].vote_average` | number | The average user rating, on a scale of 0–10. |
| `results[].vote_count` | integer | The number of user votes the `vote_average` is based on. |
| `total_pages` | integer | The total number of pages of results available. |
| `total_results` | integer | The total number of similar movies found. |

## Example response

```json
{
    "page": 1,
    "results": [
        {
            "adult": false,
            "backdrop_path": "/mWzgMPlQcFZ6lZ449673LS2aCHX.jpg",
            "genre_ids": [10751, 16, 28, 878],
            "id": 251768,
            "title": "JLA Adventures: Trapped in Time",
            "original_language": "en",
            "original_title": "JLA Adventures: Trapped in Time",
            "overview": "Get ready for a battle of the ages when the Justice League faces off against its archenemies, the Legion of Doom, in an all-new movie from DC Comics.",
            "popularity": 3.3643,
            "poster_path": "/qchNuTbnleCtlIB8wyV03f36VuF.jpg",
            "release_date": "2014-01-21",
            "softcore": false,
            "video": false,
            "vote_average": 6.632,
            "vote_count": 266
        },
        {
            "adult": false,
            "backdrop_path": "/xzi0mSJJU0de8sXn1d6S4ahzzr.jpg",
            "genre_ids": [35],
            "id": 252680,
            "title": "Moms' Night Out",
            "original_language": "en",
            "original_title": "Moms' Night Out",
            "overview": "Yearning for an evening without their kids, some friends plan a night out. But to do this, their husbands need to watch the kids. What can go wrong?",
            "popularity": 2.7338,
            "poster_path": "/gP97yU8YrVZY2yLxTwsicS8KuSe.jpg",
            "release_date": "2014-03-25",
            "softcore": false,
            "video": false,
            "vote_average": 5.606,
            "vote_count": 312
        }
        // Response truncated for readability — 20 results are returned per page.
    ],
    "total_pages": 12183,
    "total_results": 243646
}

```

</details>

## My Initial Take

Honestly, it did a lot better than I expected for a first draft. It flagged issues appropriately both before and after drafting, and asked for confirmation before proceeding. For example, Claude flagged that it wouldn’t be able to meet the “Test the endpoint first” requirement in the skill file, because it doesn’t have an authorization token. It proposed a couple options: it would make inferences from other TMDb documentation, or I could provide real request and response examples. I was planning on the latter anyway, but I was glad to see it flagged that potential issue before it even started.

## What Changes Did I Make and Why?
Claude gave me a pretty good draft, so my changes were fairly minor; it helps that TMDb already has robust documentation for Claude to reference.

I did some rewrites in the description to tighten it up. The AI-draft felt skewed towards a less experienced audience, which I appreciate, but the initial information the reader encounters should be clear and concise. No fluff necessary for describing what the endpoint returns. Claude had also included some redundancy in both paragraphs referencing how similarity is calculated, so I consolidated that in the second paragraph as useful, but not imperative, context.

Scanning through the response fields, I was pleased to see how consistent the AI draft was, but I noticed some field types were listed as string or null. It’s not technically incorrect, but for scannability having a single word descriptor for the field type is much cleaner. Plus, including a short sentence explaining the presence of a null fits nicely in the description column.

Where I spent the most time reviewing the draft was for accuracy. Claude correctly flagged the softcore field as it wasn’t able to find it in the official documentation or TMDb forums. I was glad to see the guardrail outlined in the skill file was working as intended. I verified by doing some searching of my own, and indeed that field doesn’t seem to be documented anywhere. After examining the API response and reading through Claude’s reasoning, I agree with the assessment of what the field likely means, and elected to keep the caveat that the field description is based on observed behavior.

One thing I had omitted in the skill file was for default values to be noted. I checked the official documentation and added the default values. To be honest, some of the default values seemed counter-intuitive to me and I was pleased when Claude flagged them as well, prompting me to verify the information.

AI can present such confident-sounding answers that I recognize the importance of human verification. Finally, I asked Claude to name all its sources, especially for the Response Fields. The Response Field descriptions all made sense, but I took the time to read through everything, ask for the sources, verify the sources were legit (mostly it had consulted official TMDb documentation, with some forum searching), and then I verified against the official documentation as well. 

## What will I do differently next time?
One of the biggest changes I’d like to experiment with is to add a section for reusable content in the skill file. There are consistent parameters used throughout TMDb’s API, so I would provide pre-defined verbiage to ensure consistency across the documentation. Similarly, I think there is cross-over in the Response Fields that could reduce redundant AI- generated content and support consistency. It’ll require a bit of thought and a bit of research and verification, but I think the payoff of consistent verbiage across the entire set of documentation will be worth it.

With each pass I’ll tinker with both my skill and style guide files, making additions and adjustments as needed. I’ll add an instruction about listing default values, and keeping field types limited to a single word (and I could even provide a pre-defined list of options for it to use). And I’ll make each file more robust by adding examples for the AI to reference.

In my next experiment, I also want to try out AI as a reviewer. By crafting specific personas I want to see if the AI will identify any gaps I may have missed, or prompt me to provide clarity as needed.

All-in-all I’m really glad I undertook this experiment. For me, the value of hands-on experience cannot be overemphasized. 

## The Final Draft

<details>

<summary>View the Final Draft</summary>

# Get Similar Movies

`GET` `https://api.themoviedb.org/3/movie/{movie_id}/similar`

Returns a list of movies similar to a specified movie. This is useful for building "you might also like" or recommendation sections in a movie app.

Because similarity is based on genres and keywords rather than deeper content analysis, results won't always be a perfect match. Use this as a starting point for recommendations, not a precise similarity score.

## Prerequisites

All TMDb endpoints require authentication. Include your API read access token as a bearer token in the request header (see **Request headers** below).

## Base URL

```
https://api.themoviedb.org/3
```

## Request headers

| Header | Required | Description |
|---|---|---|
| `Authorization` | Required | Your API read access token, formatted as `Bearer {token}`. |

## Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `movie_id` | integer | Required | The ID of the movie you want similar results for. |

## Query parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `language` | string | Optional | The language for the response, as an ISO 639-1 code. Defaults to `en-US`. |
| `page` | integer | Optional | The page of results to return. Defaults to `1`. |

## Example request

```
GET https://api.themoviedb.org/3/movie/533535/similar?language=en-US&page=1
Authorization: Bearer {your_token}
```

## Response fields

| Field | Type | Description |
|---|---|---|
| `page` | integer | The current page of results. Defaults to 0 if omitted from the response. |
| `results` | array of objects | The list of movies similar to the requested movie. |
| `results[].adult` | boolean | Whether the movie is flagged as adult content. Per TMDb documentation, default value is `true`, however most results will return `false`. |
| `results[].backdrop_path` | string | The file path for the movie's backdrop image, relative to TMDB's image base URL. `null` if no backdrop is available. |
| `results[].genre_ids` | array of integers | The IDs of the genres associated with the movie. A full list of genre IDs and their corresponding names can be found using the `GET /genre/movie/list` endpoint |
| `results[].id` | integer | The unique TMDB ID for the movie. Defaults to 0 if omitted from the response. |
| `results[].original_language` | string | The original language of the movie, as an ISO 639-1 code. |
| `results[].original_title` | string | The movie's title in its original language. |
| `results[].overview` | string | A short plot summary of the movie. |
| `results[].popularity` | number | A relative popularity score TMDB calculates based on factors like votes, views, and watchlist adds. Defaults to 0 if omitted from the response. |
| `results[].poster_path` | string | The file path for the movie's poster image, relative to TMDB's image base URL. `null` if no poster is available. |
| `results[].release_date` | string | The movie's release date, in `YYYY-MM-DD` format. |
| `results[].softcore` | boolean | **Inferred, not in official documentation.** Appears to flag content of a softcore-adult nature, similar in purpose to `adult`. This field isn't listed in TMDB's published schema for this endpoint, so treat this definition as observed behavior rather than confirmed intent. |
| `results[].title` | string | The movie's title, localized to the requested `language`. |
| `results[].video` | boolean | Whether the entry has an associated video (for example, a direct-to-video release). Per TMDb documentation, default value is `true`, however most results will return `false`. |
| `results[].vote_average` | number | The average user rating, on a scale of 0–10. Defaults to 0 if omitted from the response. |
| `results[].vote_count` | integer | The number of user votes the `vote_average` is based on. Defaults to 0 if omitted from the response. |
| `total_pages` | integer | The total number of pages of results available. Defaults to 0 if omitted from the response. |
| `total_results` | integer | The total number of similar movies found. Defaults to 0 if omitted from the response. |

## Example response

```json
{
    "page": 1,
    "results": [
        {
            "adult": false,
            "backdrop_path": "/mWzgMPlQcFZ6lZ449673LS2aCHX.jpg",
            "genre_ids": [10751, 16, 28, 878],
            "id": 251768,
            "title": "JLA Adventures: Trapped in Time",
            "original_language": "en",
            "original_title": "JLA Adventures: Trapped in Time",
            "overview": "Get ready for a battle of the ages when the Justice League faces off against its archenemies, the Legion of Doom, in an all-new movie from DC Comics.",
            "popularity": 3.3643,
            "poster_path": "/qchNuTbnleCtlIB8wyV03f36VuF.jpg",
            "release_date": "2014-01-21",
            "softcore": false,
            "video": false,
            "vote_average": 6.632,
            "vote_count": 266
        },
        {
            "adult": false,
            "backdrop_path": "/xzi0mSJJU0de8sXn1d6S4ahzzr.jpg",
            "genre_ids": [35],
            "id": 252680,
            "title": "Moms' Night Out",
            "original_language": "en",
            "original_title": "Moms' Night Out",
            "overview": "Yearning for an evening without their kids, some friends plan a night out. But to do this, their husbands need to watch the kids. What can go wrong?",
            "popularity": 2.7338,
            "poster_path": "/gP97yU8YrVZY2yLxTwsicS8KuSe.jpg",
            "release_date": "2014-03-25",
            "softcore": false,
            "video": false,
            "vote_average": 5.606,
            "vote_count": 312
        }
        // Response truncated for readability — 20 results are returned per page.
    ],
    "total_pages": 12183,
    "total_results": 243646
}
```

</details>