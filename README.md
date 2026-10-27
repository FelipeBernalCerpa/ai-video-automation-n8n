# AI video automation (n8n)

An n8n workflow that produces and publishes short vertical videos about AI on its own, using an AI avatar. I built it to learn how to chain agents, video APIs and publishing into one pipeline.

**Disclosure:** the channel it feeds uses an AI-generated avatar, with a cloned face and voice of mine. Topics, scripts and visuals are proposed by AI agents inside the workflow, under rules I wrote. Output example: [YouTube channel](https://www.youtube.com/channel/UCK5vAxJgzzY9MPzQGbsi3EA).

## How it works

**1. Trigger.** A schedule fires every morning and picks the content pillar for the day (news, myths, teaching, applied AI, business and health, viral).

**2. Topic.** The workflow reads a Google Sheet with ideas and a list of topics already published, so it does not repeat itself.

**3. Writing.** An orchestrator agent coordinates sub-agents: a news researcher, a title generator, a copywriter, a visual prompt writer and a fact-checker with web search. A script is only used after the fact-check approves it.

**4. Video.** HeyGen creates the avatar video from the script. The workflow waits and checks until it is ready.

**5. Edit.** Creatomate adds animated subtitles and renders the final vertical video.

**6. Publish.** The video is uploaded to YouTube with title, description and tags, and the Sheet row is marked as published.

## Set it up

Import `content-creation-workflow.json` into n8n. Create your own credentials for Google Sheets, OpenAI, SerpApi, HeyGen, YouTube and a Header Auth for HeyGen. Replace every placeholder in the file: `YOUR_GOOGLE_SHEET_ID`, `YOUR_CREATOMATE_API_KEY`, `YOUR_HEYGEN_AVATAR_ID`, `YOUR_HEYGEN_TALKING_PHOTO_ID` and `YOUR_HEYGEN_VOICE_ID`. Keep API keys in n8n credentials, never inside a node.

## Notes

The agent prompts are in Spanish because the channel is in Spanish. The workflow publishes without human review, so I recommend setting the YouTube privacy to private or adding an approval step before you run it.
