# Level Data Models & Schemas

```swift
struct LevelDataModel: Identifiable, Codable {
    let id: Int
    let title: String
    let imageName: String
    let difficulty: String
    var isUnlocked: Bool
}
```
