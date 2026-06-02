# Playlist Chaos

Your AI assistant tried to build a smart playlist generator. The app runs, but some of the behavior is unpredictable. Your task is to explore the app, investigate the code, and use an AI assistant to debug and improve it.

This activity is your first chance to practice AI-assisted debugging on a codebase that is slightly messy, slightly mysterious, and intentionally imperfect.

You do not need to understand everything at once. Approach the app as a curious investigator, work with an AI assistant to explain what you find, and make targeted improvements.

---

## How the code is organized

### `app.py`  

The Streamlit user interface. It handles things like:

- Showing and updating the mood profile  
- Adding songs  
- Displaying playlists  
- Lucky pick  
- Stats and history

### `playlist_logic.py`  

The logic behind the app, including:

- Normalizing and classifying songs  
- Building playlists  
- Merging playlist data  
- Searching  
- Computing statistics  
- Lucky pick mechanics

You will need to look at both files to understand how the app behaves.

---

## What you will do

### 1. Explore the app  

Run the app and try things out:

- Add several songs with different titles, artists, genres, and energy levels  
- Change the mood profile  
- Use the search box  
- Try the lucky pick  
- Inspect the playlist tabs and stats  
- Look at the history  

As you explore, write down at least five things that feel confusing, inconsistent, or strange. These might be bugs, quirks, or unexpected design decisions.

### 2. Ask AI for help understanding the code  

Pick one issue from your list. Use an AI coding assistant to:

- Explain the relevant code sections  
- Walk through what the code is supposed to do  
- Suggest reasons the behavior might not match expectations  

For example:

> "Here is the function that classifies songs. The app is mislabeling some songs. Help me understand what the function is doing and where the logic might need adjustment."

Before making changes, summarize in your own words what you think is happening.

### 3. Fix at least four issues  

Make improvements based on your investigation.

For each fix:

- Identify the source of the issue  
- Decide whether to accept or adjust the AI assistant's suggestions  
- Update the code  
- Add a short comment describing the fix  

Your fixes may involve logic, calculations, search behavior, playlist grouping, lucky pick behavior, or anything else you discover.

### 4. Test your changes  

After each fix, try interacting with the app again:

- Add new songs  
- Change the profile  
- Try search and stats  
- Check whether playlists behave more consistently  

Confirm that the behavior matches your expectations.

### 5. Optional stretch goals  

If you finish early or want an extra challenge, try one of these:

- Improve search behavior  
- Add a "Recently added" view  
- Add sorting controls  
- Improve how Mixed songs are handled  
- Add new features to the history view  
- Introduce better error handling for empty playlists  
- Add a new playlist category of your own design  

---

## Tips for success

- You do not need to solve everything. Focus on exploring and learning.  
- When confused, ask an AI assistant to explain the code or summarize behavior.  
- Test the app often. Small experiments reveal useful clues.  
- Treat surprising behavior as something worth investigating.  
- Stay curious. The unpredictability is intentional and part of the experience.

When you finish, Playlist Chaos will feel more predictable, and you will have taken your first steps into AI-assisted debugging.

## Bugs Found & Fixed

| # | Location | Bug | Fix | Status |
|---|----------|-----|-----|--------|
| 1 | `playlist_logic.py` → `search_songs` | Containment check was reversed (`value in q`), so partial searches like "AC" never matched "AC/DC". | Changed to `q in value` so the query is matched against the field value. | ✅ Fixed |
| 2 | `playlist_logic.py` → `random_choice_or_none` | `random.choice()` was called with no empty-list guard, raising `IndexError` on empty playlists despite the function promising `None`. | Added an `if not songs: return None` guard. | ✅ Fixed |
| 3 | `playlist_logic.py` → `compute_playlist_stats` | Hype ratio was computed from hype songs only, making the metric unbalanced. | Changed to `len(hype) / total` across all songs. | ✅ Fixed |
| 4 | `playlist_logic.py` → `compute_playlist_stats` | Average energy was computed from hype songs only. | Changed to average over all songs. | ✅ Fixed |
| 5 | `playlist_logic.py` → `history_summary` | All picks were defaulting toward "Mixed" instead of counting their actual mood. | Valid moods now increment their own count; only missing/invalid moods fall back to "Mixed". | ✅ Fixed |
| 6 | `app.py` → `stats_section` | The playlist stats section was rendering twice (once near the top, once at the bottom). | Removed the duplicate render and refactored the section for a cleaner UI. | ✅ Fixed |

## TF Summary

Core concepts that students needed to understand for the first week tinker is how to enter into a codebase and start gaining understanding of the functionality of the different files/functions. This understanding phase can be accelerated with the use of CoPilot or any other AI tool(claude code, gemini, etc.). Another core concept is how to debug and refactor code to make the code readable and functional. Students will most likely struggle with the beginning where they need to clone the repo and have everything setup properly. I expect some students to not have their environment setup properly. Students might also struggle with learning how to debug with Copilot, especially if they rarely used Copilot or other AI tooling to debug their code.

AI was helpful with understanding the code, albeit some of the explanation was still a little confusing. Students might be mislead by Copilot when  trying to debug. For example, I had an issue where the playlist stats section was displayed twice. One near the top, and the near the bottom of the page(where the Playlist stats section was supposed to be located). I asked Copilot to resolve the issue for me, and Copilot led me to check multiple different functions until finding the one that was causing the issue. Though that might have been due to me giving vague instructions to the Copilot. One way I would guide a student without giving the answer is to help them craft the prompt they are going to send to Copilot. Prompting correctly is very important to fully leveraging AI tools like Copilot.