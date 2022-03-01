# ovos play examples

## "importable" ovos play content packages 

Specific information about entities:

- [Library Structure](Library.md)
- [Decks and Cards](Decks-and-Cards.md)
- [Example Content Package structure for importer](content-package.json)

### JSON Schema

The current JSON Schema for ovos play content packages,
is available at https://app.ovosplay.com/api/import-schema.json

You can add a `"$schema": "https://app.ovosplay.com/api/import-schema.json"` property to your content package json file,
to get validation/auto-completion in your IDE.

#### Meta Information

Every content packages `data.json` should include a `meta` information object.

It contains the following properties:

- `internal`: **boolean** Whether this content package has been created by ovos play code.
- `tenant`: *(optional)***string** the tenant from which the content package was created
- `instanceTag`: *(optional)***string** the instance tag is used to differentiate between different tenant instances or stages of content (e.g. `stage`, `production`)
- `time`: *(optional)***string** timstamp of when the content package has been created (e.g. `""2022-01-31T11:28:39.182Z"`)
- `version`: *(optional)***number** the version of the exporter which created this content package

### Content Structure

With the content importer, you can create a library structure,
decks and cards.

Example without any actual content: 

```json
{
  "$schema": "https://app.ovosplay.com/api/import-schema.json",
  "meta": {
    "time": "2022-02-16T09:02:41.513Z",
    "version": 3
  },
  "cards": [],
  "decks": [],
  "library": []
}
```

### `refId`

In order to allow ovos play to recognize if imported content should be updated instead of added, the `refId` property is used.

When the `refId` property of an element does not change, and it already exists in ovos play, the imported content will update the existing item instead of create a new one.

The format should be like this:

`"refId": "clientName/source:itemType:itemId"`

In ovos play, this is stored as the `external_reference_id` for each imported element.
