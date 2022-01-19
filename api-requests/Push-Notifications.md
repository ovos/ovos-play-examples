# Push Notifications

## Get a list of push notification log entries

**Requires permission:** `admin.push_notifications.view`

```gql
  query notifications($filters: FilterInput) {
    pushNotificationLogs(filters: $filters) {
      results {
        id
        user
        type
        # data contains a stringified json object of the push notifications properties
        data
        created_at
        processed_at
        success
        failure
        errors
      }
    }
  }
```

## Send a push notification to a user

**Requires permission:** `admin.push_notifications.create`

```gql
  mutation createNotification {
    createPushNotifications(data: [
      { title: "Push Title", description: "Push Description", path: "/dashboard/library", userIds: [1] }
    ]) {
      id
    }
  }
```