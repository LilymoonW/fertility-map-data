
# States Dictionary

The U.S. states data dictionary is stored in a separate JSON file due to GoDaddy's HTML character limits.

Hosted on GitHub: [https://lilymoonw.github.io/fertility-map-data/statesData.json](https://lilymoonw.github.io/fertility-map-data/statesData.json)

This file contains all fertility coverage, exemption, legislation, and action data used to populate the map and side panel.

## How to Modify or Replace the JSON

### Option 1: Use Your Own Version

1. Copy the current JSON from the URL above
2. Make your desired modifications
3. Host the file on your own website or GitHub Pages
4. Replace this line in your code:

   ```javascript
   fetch("https://lilymoonw.github.io/fertility-map-data/statesData.json") // MODIFY CODE HERE
   ```

   With:
   ```javascript
   fetch("https://yourusername.github.io/your-repo/statesData.json")
   ```

### Option 2: Modify the Existing JSON

If you'd like to edit the existing shared JSON, request access to the GitHub repository and submit a pull request or issue.

## State Object Format

Each key in the JSON object represents a U.S. state or territory, using all lowercase with the exception of `puertoRico` and `districtOfColumbia` formatting (e.g., `newyork`, `puertoRico`).

```javascript
{
  "texas": {
    // state object
  },
  "utah": {
    // state object
  }
}
```

Each state/territory has the following structure:

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Full name of the state or territory |
| `legislatureUrl` | string | Official website of the state legislature |
| `currentLaws` | string[] | List of law references or external links (optional) |
| `currentCoverage` | string[] | Summary of current fertility insurance coverage (optional) |
| `exemptions` | string[] | Specific exemption clauses for insurance coverage (optional) |
| `fertilityPreservation` | string[] | Details of preservation-related policies (optional) |
| `billsInProgress` | object[] | Legislative proposals under consideration (optional) |
| `takeAction` | string[] | Suggested advocacy actions for users |
| `claimInfo` | string | Link to file insurance-related claims or complaints |
| `factSheet` | string | Title of the downloadable resource |
| `factSheetUrl` | string | URL to the official fact sheet PDF or webpage |
| `lastUpdated` | string | Timestamp of last known data verification (e.g., "April 2025") |

### Bills Format (`billsInProgress`)

```javascript
{
  "title": "string",
  "description": "string",
  "status": "string",
  "link": "string" // URL to full bill text or tracking site
}
```

## State Card UI/UX

The `renderStateCard(stateKey)` function dynamically generates and injects an HTML card into the DOM based on fertility healthcare insurance coverage data for a given U.S. state or territory.

### Conditional Rendering

- Arrays are checked with `.length` to avoid rendering empty sections
- `billsInProgress` renders a fallback message if empty
- All external links use `target="_blank"` and `rel="noopener noreferrer"` for security
```
