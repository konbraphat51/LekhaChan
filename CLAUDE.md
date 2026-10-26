# CLAUDE.md v1.0.0

Check the newest version in [Gist](https://gist.github.com/konbraphat51/af909a374c59d306c2d2b3fd7788507e) every Monday (Last checked: 2026/10/26). If newer, replace `## User Requests` with the newest document and update the version number.

## User Requests

- Write SOLID, readable, and maintainable code
- Put system documents in `/Docs/`, research notes (if user ordered you to research) in `/ResearchNotes/`
- Write comments in English
    - Comments should be concise. Should be only single line per topic.
        - There is NO need to leave comments for each code update.
            - ex: "This code is left because of..."
            - ex: "This code is deleted because of..."
        - Be aware if the code readers would prefer to read your comments, or it is just noise for them.
    - Write comments for the responsibility of the file itself at the top
    - Write comments for each public class/method/variable
        - If Python, write in docstring format
        - If C#, write in XML format
        - If TypeScript, write in TSDoc format

```python:sample.py
def transcribe(
    self,
    all_pages: list[Image],
    blocker_result: BlockerResult,
) -> TranscriptionResult:
    """Transcribes every TEXT block of blocker_result, cropped from all_pages.

    Args:
        all_pages: Every page image, indexed by Block.page_number.
        blocker_result: The blocks detected by a Blocker, to be transcribed.
    """
    transcriptions: list[TranscriptionBlock] = []

    # for each block...
    for block in blocker_result.blocks:
        # ...OCR the block

        # if the block is not text...
        if block.block_type != BlockType.TEXT:
            # ...skip
            continue

        # image extraction
        block_image = self._extract_block_image(all_pages[block.page_number], block)

        # transcribe the block image
        text = self._ocr_block_image(block_image)
        transcriptions.append(TranscriptionBlock(block, text))

    return TranscriptionResult(transcriptions)
```

- Prepare English and Japanese versions for all system documents.
    - Make English version as the primary version, and Japanese version as the secondary version.
        - ex: `README.md` (English) and `README.ja.md` (Japanese)

- For research notes (if ordered), only either language is allowed. Match with the language of the user prompt.
    - Files in `/ResearchNotes` created by Claude must start from `YYYYMMDD_` prefix.
- all in-UI text should be in English by default, but support Japanese localization.
- Everytime updated the code, check all documents and update them if necessary.
- Debug the frontend by yourself
- Make granular commits for each unit of implementation. One commit per small, self-contained unit. Do not bundle a whole subsystem into one commit. Commit each unit as soon as its checks pass.
    - Set Angular Conventional commit message prefixes.
        - For update in `/ResearchNotes/`, set prefix as `resn:`
- If you use Python
    - Use `uv` for package management
    - Enable strict typing
    - Add appropriate package for better code/quality
- If you use JavaScript/TypeScript
    - Use `pnpm` for package management
    - Add appropriate package for better code/quality
    - Use Vue for frontend
        - Granular components are preferred.
    - Write in Single File Component style, such as

```vue
<template>HTML</template>
<script>
export default {
  name:...
}
</script>
<style scoped></style>
```

- Write documents to understand the code architecture. Such as: class diagram, sequence diagram...
- In `/README.md`, write:
    - System Name as H1
    - Easy description of what system does
    - How to setup from `git clone`
    - How to run for second time and later
    - Important CLIs

- If API keys or other enviroment variables, read from `.env`
    - git ignore `.env`
    - create `.env.example`

### Naming Conventions

#### For All Languages

- Directory Names: UpperCamelCase
- File Names: UpperCamelCase
- Class Names: Must be Noun. Must be postpositive (ex: `AppleGreen`, not `GreenApple`)
- Function Names: Must be verb. Start from verb (ex: `EatApple()`, not `AppleEater()`)
- Variable Names: Basically noun, but follow general conventions (ex: `is` for booleans). Make it postpositive when noun.

#### For Python

- Class Names: UpperCamelCase
- Function Names: snake*case. Privates starts from `*`
- Variable Names: snake*case. Privates starts from `*`

#### For C#

- Class Names: UpperCamelCase
- Function Names: UpperCamelCase
- Variable Names: lowerCamelCase
- Property Names: lowerCamelCase
- Enum Names: UpperCamelCase

## Claude Notes

=Claude can freely edit below this line. Use this area to share project knowledge throught different chat sessions. Capture conventions, structure, commands, and gotchas so that agents joining later stay consistent with existing decisions.=
