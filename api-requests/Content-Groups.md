# API Requests related to users and content packages

## Get all users related to a specific content group

This query does not need any special permissions.
Only users **directly** assigned to the given content group id will be returned.
Users which are only indirectly assigned via usergroup -> cg relation won't be returned here.

```gql
  query cgUsers {
    usersFiltered(
      filters: {
        where: [
          {
            field: "id",
            relation: "contentGroups",
            value: { intValue: 1 }
          }
        ]
      }
    ) {
      results {
        id
        username
      }
    }
  }
```