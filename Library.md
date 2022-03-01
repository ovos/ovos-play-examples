# Library

The library structure is the place where decks are assigned to topics, which then are visible for users in the apps.

Individual library items can have different types, which are described below.

- `TOPIC`: A topic acts as a container for different library items (such as decks, sections or separators). A topic can only be defined on the top level and can't be nested.

- `DECK`: A library item of type `DECK` relates to a `deck` element. It must be assigned as a child element of a `TOPIC` or a `SECTION`

- `SECTION`: A section acts as a "Phase" in ovos play. It must be assigned as a child element of a `TOPIC` and should contain any number of deck library items as children.

- `SEPARATOR`: These act as visual separators of content for regular topics (eg to visually separate decks of different context).

<!--- `EVENT`: An event is similar to a `DECK` in that it relates to a `event` and must be assigned as a child element of a `TOPIC` or a `SECTION`-->

## Referencing decks in a library item

In order to relate a library item of type `DECK` with a `deck` in the content package, you must assign it via the `refId` like this:

```json
{
  "decks": [
    {
      "refId": "client/csv:deck:1",
      "name": "An example deck",
    }
  ],
  "library": [
    {
      "refId": "client/csv:library:1",
      "type": "TOPIC",
      "name": "An example topic",
      "children": [
        {
        "refId": "client/csv:library:2",
          "type": "DECK",
          "deck": {
            "refId": "client/csv:deck:1"
          }
        }
      ]
    }
  ]
}
```