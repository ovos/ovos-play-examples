# ovos play decks and cards

When creating a content package for ovos play, you can choose between a variety of different deck and card types.

## Deck Type

```json
{
  "decks": [
    {
      "refId": "client/csv:deck:normal",
      "name": "Example",
      "type": "NORMAL",
    },
    {
      "refId": "client/csv:deck:initial",
      "name": "Example",
      "type": "INITIAL",
    },
    {
      "refId": "client/csv:deck:assessment",
      "name": "Example",
      "type": "ASSESSMENT",
    },
  ]
}
```

`NORMAL`: The default type of a deck (if omitted). Deck will need to be "explored" before it can be practiced (except if it does not have any learn cards).

`INITIAL`: All practice cards of the deck will be immediately available for the users in practice modes and duels (no prior "learning" required).

`ASSESSMENT`: The deck will be displayed and treated as an assessment. Requires cards to be assigned via `assessmentCards`.

## Link Mode

When assigning cards to a deck, you can choose between different "types" of assigning them.

```json
{
  "decks": [
    {
      "refId": "client/csv:deck:Example",
      "name": "Example",
      "points": 50,
      "duration": 5,
      "practiceCards": [
        {
          "refId": "client/csv:question:2576",
          "sort": 0
        },
      ],
      "learnCards": [
        {
          "refId": "client/csv:question:2577",
          "sort": 1
        },
      ],
      "assessmentCards": [
        {
          "refId": "client/csv:question:2578",
          "sort": 2
        }
      ]
    }
  ]
}
```

`practiceCards`: Cards available in the "practice" mode of the deck
`learnCards`: Cards available only in learn mode
`assessmentCards`: Cards available in assessment mode (requires deck type to be `ASSESSMENT`)

## Card Assets

Every cards content is stored as a `card asset`. A card might have multiple related assets, depending on its type.

A cards assets are assigned by the `assets` property (which should be an array of asset objects) on the card.

## Card Types

### Content Cards

Content cards might require user interaction in special cases, but usually do not block the user from continuing a learn or assessment session.

These cards can be linked to decks as `learnCards` or `assessmentCards`.

#### `CONTENT_TEXT`

Plain text content.

- **# Assets:** 1
- **Relevant asset fields:** `content`

#### `CONTENT_TEXT_HEADLINES`

A card which contains multiple "headlines" which have to be clicked to read by the user.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Also requires property `headlines`.

#### `CONTENT_TEXT_IMAGE`

A card with image + text.

- **# Assets:** 1
- **Relevant asset fields:** `content, file_image_id, image_scale_type`

#### `CONTENT_TEXT_VIDEO`

A card with video + text.

- **# Assets:** 1
- **Relevant asset fields:** `content, file_video_id`

#### `CONTENT_IMAGE`

A card with only an image.

- **# Assets:** 1
- **Relevant asset fields:** `file_image_id, image_scale_type`

#### `CONTENT_QUOTE`

A card with a "quote" (specially formatted text).

- **# Assets:** 1
- **Relevant asset fields:** `content`

#### `CONTENT_IFRAME`

A card which contains an iframe. Note that iframes should point to
secure URLs.

- **# Assets:** 1
- **Relevant asset fields:** `content` (should contain the iFrame URL)

#### `CONTENT_SCENE`

A more complicated type of card, which can contain many "scene backgrounds" with multiple hotspots.

**Requires `scenes` with `hotspots`** (refer to json schema for available fields)

#### `CONTENT_FLIP`

A card which has two sides of content which can be flipped.

- **# Assets:** 2
- **Relevant asset fields:** `content, file_image_id, file_audio_id, image_scale_type`

#### `CONTENT_DOCUMENT`

A card which contains a document (eg pdf).
- **# Assets:** 1
- **Relevant asset fields:** `file_id`

### Task Cards

Task cards always require user interaction to continue and may be used in practice mode.

These cards can be linked to a deck in any link mode (learn, practice, assessment).

#### `TASK_CHOICE_TEXT`

A single or multiple choice "text" card.

- **# Assets:** 1
- **Relevant asset fields:** `content`

#### `TASK_CHOICE_IMAGE``

A single or multiple choice "image" card.

- **# Assets:** 1
- **Relevant asset fields:** `content, file_image_id`

#### `TASK_FACT_OR_FICTION`

A fact/fiction type of card which can either be correct or not.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Does not need answers. Uses `correct` property on card to specify wheter content is a fact or fiction.

#### `TASK_CLOZE_CHOOSE_ANSWER`

A cloze card, where the user can choose predefined answers.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Asset content should include `{{1}}` placeholders where the number should be assigned to the `placeholder` prop in the `answers` objects (each answer can be set as correct or incorrect).

#### `TASK_CLOZE_TEXT_INPUT`

A cloze card, where the user must type answers manually.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Asset content should include `{{1}}` placeholders where the number should be assigned to the `placeholder` prop in the `answers` objects.

#### `TASK_DUAL_ROW_ORDER`

A card template where the user has to drag answers into correct order.

- **# Assets:** any #
- **Relevant asset fields:** `content`

Answers should have same length as assets.
Can use `order_matters` prop on card to specify whether the order of answers matters as well as the answer->asset combination.

#### `TASK_TEXT_INPUT`

A text input, where the user has to provide the correct answer.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Can have multiple correct answers for the "correct" value.

#### `TASK_SLOTS`

Casino like "slots" template, where the user must set the correct combination of "slots".

- **# Assets:** 1
- **Relevant asset fields:** `content`

Each answer should contain a `placeholder` number which refers to the slot number. The same slot numbers will be displayed as a vertical carousel. Each answer must also provide a file_image_id and the correct answer should be marked as `correct: true`.

### Survey Cards

These cards are similar to task cards, but do not have correct answers and can be evaluated in the admin dashboard.

#### `SURVEY_TEXT`

Free form text input, where users can enter any answer manually.

- **# Assets:** 1
- **Relevant asset fields:** `content`

#### `SURVEY_SCALE`

A scale where users can choose eg from 1 - 4.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Answers may specify `file_image_id` to overwrite the default scale smiley images.

#### `SURVEY_RADIO`

Similar to `SURVEY_SCALE` but offers only fixed answer slots.

- **# Assets:** 1
- **Relevant asset fields:** `content`

Answers may specify `file_image_id` to overwrite the default scale smiley images.

#### `SURVEY_CHOICE`

- **# Assets:** 1
- **Relevant asset fields:** `content`

Similar to the `TASK_CHOICE` template, but does not have a correct answer.