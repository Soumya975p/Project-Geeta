# API Integration Documentation

## API Details

**Base URL:** `https://sanskrit.ie/api/geeta.php`

### Endpoints

#### Get Chapter Verses
- **Method:** GET
- **Endpoint:** `/?q={chapter_number}`
- **Example:** `https://sanskrit.ie/api/geeta.php?q=1`
- **Description:** Returns all verses for the specified chapter number

### Chapter Information
- Total Chapters: 18 (fixed according to the Bhagavad Gita)
- Each chapter has a varying number of verses

## Implementation

### API Response Structure

The API returns data in the following format:
```json
{
  "status": 200,
  "message": "Data Listed",
  "data": [
    {
      "geeta_id": "749",
      "chapter_no": "1",
      "shlok_no": "0",  // Chapter introduction
      "lyrics": "...",
      "music": "images/music/file/479344313.mp3",
      "qr": "images/qr/G749.png"
    },
    {
      "geeta_id": "9",
      "chapter_no": "1",
      "shlok_no": "1",  // Actual verses
      "lyrics": "...",
      "music": "...",
      "qr": "..."
    }
    // ... more verses
  ]
}
```

### How It Works

1. **Chapter Selection:**
   - User clicks on a chapter diamond (1-18)
   - `viewChapter()` function is triggered
   - Chapter number is stored and view switches to 'verses'
   - Page smoothly scrolls to top

2. **API Call:**
   - When `VerseGrid` component mounts, it automatically fetches verses
   - API endpoint: `https://sanskrit.ie/api/geeta.php?q={chapterNumber}`
   - Response structure: `{status: 200, message: "Data Listed", data: [...]}`
   - Filters out `shlok_no: "0"` (chapter introduction)
   - Extracts unique verse numbers from `shlok_no` field
   - Verse scrolls are dynamically generated based on actual API data

3. **Fallback Mechanism:**
   - If API fails, uses default verse counts:
     ```javascript
     [47, 72, 43, 42, 29, 47, 30, 28, 34, 42, 55, 20, 34, 27, 20, 24, 28, 78]
     ```

4. **Smooth Scrolling:**
   - Automatic scroll to top when switching between chapters and verses
   - Smooth behavior for better UX

### Files Modified

1. **`src/lib/VerseGrid.svelte`**
   - Added API integration with `fetch()`
   - Added loading and error states
   - Dynamic verse generation based on API response
   - Passes chapter number to play event

2. **`src/lib/GitaPage.svelte`**
   - Enhanced smooth scrolling
   - Updated play handler to include chapter context
   - Added timeout for scroll to ensure DOM is ready

## Testing the Integration

1. Start the development server:
   ```bash
   npm run dev
   ```

2. Open the application in browser

3. Click on any chapter (1-18)

4. Observe:
   - API call in browser Network tab
   - Loading message briefly appears
   - Verses are displayed based on API response
   - If API is down, default verses are shown

## GitHub Repository

**Repository:** https://github.com/Soumya975p/Project-Geeta
**Branch:** main

Designers can check the progress at the above link. The repository includes:
- Full source code with API integration
- Responsive design with diamond chapter layout
- Verse grid system
- Audio popup functionality (placeholder for now)

## Next Steps

1. **Audio Integration:**
   - Add actual audio files to `/public/audio/` directory
   - Update audio paths in `handlePlay()` function
   - Consider using an audio API if available

2. **API Response Handling:**
   - Review actual API response structure when available
   - Update parsing logic if needed
   - Add more detailed error handling

3. **Verse Content:**
   - Display actual verse text in popup
   - Add translation if available from API
   - Add verse explanations if provided

4. **Performance:**
   - Add caching for API responses
   - Implement loading skeletons
   - Optimize image loading
