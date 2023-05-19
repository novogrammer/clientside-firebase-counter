
# clientside-firebase-counter

クライアントサイドでfirebaseのカウンターを実現する
firestoreを使う


# セキュリティルール
以下のセキュリティルールを設定しておく、

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if false;
    }  
    match /counters/{counterId} {
      allow read: if true;
      allow write: if resource.data.count + 1 == request.resource.data.count;
    }
  }
}
```

