# SendbirdUI

A description of this package.

# How to use?

> **IMPORTANT** Please see each previews file in *ChannelList* folder. e.g. `UserMessage.Previews.swift`

## Messages

### User message modifier for SBDUseMessage

```swift
.userMessageStyle(_:)
```

**Parameter**

`style`: The style of user message view that is a type of `UserMessageModifier.Style`

```swift
public enum UserMessageModifier.Style {
    case body
    case date
    case receipt
    case senderName
    case senderProfile
}
```

**Exmaple**

```swift
// Profile image of sender
Image(systemName: "person.crop.circle.fill")
    .resizable()
    .userMessageStyle(.senderProfile)
    
// The nickname of sender
Text(message.sender?.nickname ?? "No_name")
    .userMessageStyle(.senderName)
    
// The message bubble
Text(message.message)
    .userMessageStyle(.body)
```

## Channels

> **NOTE** Currently, it supports `SBDGroupChannel` only.

### Layout for the grid style

```swift
ChannelGrid<Channel: SBDGroupChannel>(limit:order:content:)
```

**Parameters**

- `limit`: The limit of channel list query. The default value is `20`.
- `order`: The order of grid items that is a type of `ChannelGrid.Order`.
- `content`: The content of the grid style layout. The closure has `SBDGroupChannel` object as a parameter value.

```swift
public enum ChannelGrid.Order {
    case chronological
    case latestLastMessage
    case channelNameAlphabetical
    case channelMetaDataValueAlphabetical
}
```

**Exmaple**

```swift
ChannelGrid { channel in
    // Description of content using `channel`
    AsyncImage(url: URL(string: channel.coverUrl ?? "")) { image in
        image
            .resizable()
            .channelRowStyle(.coverImage(100, .group))
    }
}
```

### Layout for the list style

Please refer to *"Layout for the grid style"*.


### Channel row modifier for SBDGroupChannel

```swift
.channelRowStyle(_:)
```

**Parameter**

`style`: The style of channel row item view that is a type of `ChannelRowModifier.Style`

```swift
public enum ChannelRowModifier.Style {
    case title(_ channelType: ChannelType)
    case coverImage(_ size: CGFloat, _ channelType: ChannelType)
    case memberCount(_ channelType: ChannelType)
    case lastMessage(_ channelType: ChannelType)
    case date(_ ChannelType: ChannelType)
}
```

**Exmaple**

```swift
// The cover image of channel
ChannelImage(from: channel)
    .channelRowStyle(.coverImage(100, .group))
    
// The name of channel
Text(channel.name)
    .channelRowStyle(.title(.group))
```
