# **HuggingFace User Stats**

A single-page web application for viewing detailed statistics of any HuggingFace user account. Displays models, datasets, spaces, lifetime downloads, monthly downloads, and likes in a clean, tree-structured interface.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Token Configuration](#token-configuration)
- [Interface Guide](#interface-guide)
- [Sorting and Filtering](#sorting-and-filtering)
- [Copy and Export](#copy-and-export)
- [Featured Users](#featured-users)
- [Technical Details](#technical-details)
- [API Endpoints Used](#api-endpoints-used)
- [Browser Support](#browser-support)
- [Limitations](#limitations)
- [License](#license)
- [Author](#author)

## Overview

HF User Stats is a lightweight, client-side tool that fetches and presents comprehensive statistics for any public (or private, with a token) HuggingFace user account. It requires no backend server, no build step, and no dependencies beyond a modern web browser. All data is fetched directly from the HuggingFace API.

## Features

- **User Profile Display** -- Shows user avatar, username, and full name.
- **Aggregate Statistics** -- Total models, datasets, and spaces at a glance.
- **Lifetime Downloads** -- All-time download counts for models and datasets.
- **Monthly Downloads** -- Downloads from the last 30 days for models and datasets.
- **Likes** -- Total like counts across all repository types.
- **Tree View** -- File-explorer-style hierarchical listing of all repositories.
- **Sorting** -- Sort by all-time downloads, monthly downloads, likes, or recency.
- **Filtering** -- Search and filter repositories by name within any tab.
- **Tab Navigation** -- Switch between models, datasets, and spaces views.
- **Dark and Light Theme** -- Toggle between themes with preference saved to local storage.
- **Token Support** -- Optional HuggingFace access token for private repositories and improved rate limits.
- **Copy to Clipboard** -- Copy individual repository IDs or the entire tree output as plain text.
- **Pagination Handling** -- Automatically fetches all pages of results for users with large numbers of repositories.
- **Pipeline Tag Icons** -- Models display context-appropriate icons based on their pipeline tag (text generation, image classification, speech recognition, and others).
- **Responsive Design** -- Works on desktop and mobile screens.
- **No Build Required** -- Single HTML file with inline CSS and JavaScript.

## Getting Started

### Option 1: Direct File

1. Download the `index.html` file.
2. Open it in any modern web browser.

### Option 2: Local Server

```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .
```

Then navigate to `http://localhost:8000` in your browser.

### Option 3: Deploy

Upload the single HTML file to any static hosting service such as GitHub Pages, Netlify, Vercel, or Cloudflare Pages.

## Usage

1. Enter a HuggingFace username in the input field (for example, `prithivMLmods`, `TheBloke`, `merve`).
2. Click **Fetch Stats** or press Enter.
3. View the user profile, aggregate statistics, and detailed repository listings.
4. Use tabs to switch between Models, Datasets, and Spaces.
5. Use sort and filter controls to find specific repositories.

The username is stored in the URL hash, so you can bookmark or share links directly:

```
https://your-deployment.com/#prithivMLmods
```

## Token Configuration

A HuggingFace access token is optional but recommended for the following reasons:

- **Private Repositories** -- Access user repositories that are not public.
- **Higher Rate Limits** -- Avoid API throttling when fetching users with many repositories.
- **Accurate Lifetime Stats** -- Some statistics fields require authentication to return complete data.

### Setting a Token

1. Click the **Token** button in the header.
2. Paste your HuggingFace access token (starts with `hf_`).
3. Click **Save**.

The token is stored in your browser's local storage. It is never sent to any server other than the HuggingFace API.

### Generating a Token

1. Go to [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).
2. Create a new token with `read` access.
3. Copy the token and paste it into the application.

### Clearing a Token

Click the **Clear** button in the token panel to remove the stored token.

## Interface Guide

### Profile Card

Displays the user avatar (circular, with accent-colored border), username (linked to the HuggingFace profile), and full name if available. The three overview cards show total counts for models, datasets, and spaces, and can be clicked to switch tabs.

### Tab Bar

Three tabs for switching between repository types:

| Tab | Description |
|-----|-------------|
| Models | Machine learning models published by the user |
| Datasets | Datasets published by the user |
| Spaces | Gradio, Streamlit, or other interactive applications |

### Statistics Row

Shows aggregate numbers for the currently selected tab:

- **Total Count** -- Number of repositories of the selected type.
- **Downloads (All Time)** -- Cumulative downloads across all repositories (models and datasets only).
- **Downloads (Last Month)** -- Downloads in the last 30 days (models and datasets only).
- **Total Likes** -- Sum of likes across all repositories.

### Tree View

A terminal-style listing of all repositories with:

- Repository name (linked to HuggingFace)
- Pipeline tag icon (for models, mapped to 24 different task types)
- All-time download count
- Monthly download count
- Like count
- Last modified timestamp (relative format)
- Copy button for the repository ID

## Sorting and Filtering

### Sort Options for Models and Datasets

| Sort | Description |
|------|-------------|
| Downloads (All Time) | Highest lifetime downloads first |
| Downloads (Last Month) | Highest monthly downloads first |
| Most Liked | Highest like count first |
| Most Recent | Most recently modified first |

### Sort Options for Spaces

| Sort | Description |
|------|-------------|
| Most Liked | Highest like count first |
| Least Liked | Lowest like count first |

### Name Filter

Use the search field in the filter bar to filter repositories by name. Matching text is highlighted in the tree view with an accent-colored background.

## Copy and Export

### Copy Individual ID

Hover over any repository in the tree view and click the copy icon to copy the full repository ID (for example, `prithivMLmods/Some-Model`) to your clipboard. A green checkmark confirms the copy.

### Copy Full Tree

Click the **Copy Tree** button in the tree header to copy the entire listing as formatted plain text, including aggregate statistics. The output format:

```
prithivMLmods -- 25 Models
|-- Model-Name-A (down-arrow 1.2M all down-arrow 234.5K /mo heart 1,234)
|-- Model-Name-B (down-arrow 890.3K all down-arrow 123.4K /mo heart 987)
L-- Model-Name-C (down-arrow 567.8K all down-arrow 89.1K /mo heart 654)

Total Downloads (All Time): 12,345,678
Total Downloads (Last Month): 1,234,567
Total Likes: 9,876
```

## Featured Users

The homepage displays a curated list of featured HuggingFace users for quick access. Any valid HuggingFace username can be queried by entering it directly in the input field.

Pre-listed users include:

```
prithivMLmods, TheBloke, merve, MaziyarPanahi, multimodalart,
thomwolf, julien-c, lysandre, osanseviero, pcuenq, clem,
lhoestq, sayakpaul, mlabonne, mradermacher
```

& more !!

## Technical Details

### Architecture

- **Single HTML file** -- No external dependencies beyond CDN-loaded fonts and icons.
- **Client-side only** -- All API calls are made directly from the browser to the HuggingFace API.
- **No framework** -- Vanilla JavaScript with direct DOM manipulation.
- **Responsive CSS** -- Custom properties (CSS variables) for theming with media queries for mobile layouts.

### External Resources

| Resource | Source |
|----------|--------|
| Font Awesome 6.4.0 | cdnjs.cloudflare.com |
| Inter font | Google Fonts |
| JetBrains Mono font | Google Fonts |

### Data Flow

1. User enters a username.
2. Application fetches the user profile from the HuggingFace API.
3. Application fetches all models, datasets, and spaces in parallel using `Promise.allSettled`.
4. If like counts are missing from the list endpoints (all zeros), individual detail endpoints are queried in batches of 10 with concurrent requests within each batch.
5. All data is stored in a client-side state object.
6. The UI renders from the state object without further API calls until a new fetch is initiated.

### State Management

The application maintains a single state object:

```javascript
{
    username: '',      // Current username being viewed
    profile: null,     // User profile data from the API
    models: [],        // Array of model objects
    datasets: [],      // Array of dataset objects
    spaces: [],        // Array of space objects
    activeTab: 'models',           // Currently selected tab
    activeFilter: 'downloads-alltime', // Current sort order
    filterText: '',    // Current name filter text
}
```

### Local Storage Keys

| Key | Purpose |
|-----|---------|
| `hf_token` | HuggingFace access token |
| `hfstat_theme` | Theme preference (`light` or `dark`) |

### Pipeline Tag Icon Mapping

Models display task-specific icons based on their `pipeline_tag` field. The following mappings are supported:

| Pipeline Tag | Icon |
|-------------|------|
| text-generation | Message bubble |
| text2text-generation | Language |
| text-classification | Tags |
| token-classification | Font |
| question-answering | Question circle |
| fill-mask | Mask |
| summarization | Compress |
| translation | Globe |
| conversational | Comments |
| image-classification | Image |
| object-detection | Vector square |
| image-segmentation | Puzzle piece |
| text-to-image | Magic wand |
| image-to-text | File lines |
| automatic-speech-recognition | Microphone |
| text-to-speech | Volume high |
| audio-classification | Music note |
| feature-extraction | Layer group |
| sentence-similarity | Left-right arrows |
| reinforcement-learning | Gamepad |
| image-to-image | Images |
| video-classification | Film |
| depth-estimation | Mountain |
| zero-shot-classification | Bullseye |

Models with unrecognized or missing pipeline tags display a default cube icon.

## API Endpoints Used

| Endpoint | Purpose |
|----------|---------|
| `GET /api/users/{username}/overview` | User profile, avatar, and full name |
| `GET /api/models?author={username}` | List all models with download and like counts |
| `GET /api/datasets?author={username}` | List all datasets with download and like counts |
| `GET /api/spaces?author={username}` | List all spaces with like counts |
| `GET /api/models/{id}` | Individual model details (fallback for missing stats) |
| `GET /api/datasets/{id}` | Individual dataset details (fallback for missing stats) |

### Expand Parameters

The following expand parameters are used in list API calls to request additional fields:

- `downloadsAllTime` -- Lifetime total download count
- `downloads` -- Last 30 days download count
- `likes` -- Like count
- `lastModified` -- Last modification timestamp
- `createdAt` -- Creation timestamp

## Browser Support

| Browser | Minimum Version |
|---------|----------------|
| Chrome | 80+ |
| Firefox | 78+ |
| Safari | 14+ |
| Edge | 80+ |

Requires JavaScript enabled and network access to `huggingface.co`.

## Limitations

- **Rate Limiting** -- The HuggingFace API may throttle requests for users with a very large number of repositories. Using a token mitigates this.
- **Spaces Downloads** -- The HuggingFace API does not provide download counts for Spaces. Only like counts are displayed for the Spaces tab.
- **Private Repositories** -- Private repositories require a valid access token with appropriate permissions to appear in results.
- **Avatar Resolution** -- User avatars are loaded from the profile API response. If the avatar URL is unavailable or fails to load, a colored circle with the first letter of the username is displayed as a fallback.
- **Concurrent Requests** -- Detail fetching for missing like counts is done in sequential batches of 10 to avoid overwhelming the API.
- **Download Statistics Accuracy** -- The `downloadsAllTime` field may not be available for all repositories. When unavailable, the application falls back to the `downloads` field (last 30 days) as the lifetime value, which may understate the true total.

## Differences from Organization Stats

This tool is designed specifically for individual HuggingFace user accounts rather than organizations. Key differences include:

| Feature | User Stats | Organization Stats |
|---------|-----------|-------------------|
| Profile avatar shape | Circular with accent border | Rounded square |
| Member count display | Not shown | Displayed when available |
| Organization badge | Not shown | Displayed next to name |
| API endpoint for profile | `/api/users/{name}/overview` | `/api/organizations/{name}` with fallback |
| Avatar fallback chain | Single URL from profile API | Multiple candidate URLs attempted |

## License

This project is open source. See the repository for license details.

## Author

Built by [prithivMLmods](https://huggingface.co/prithivMLmods)
