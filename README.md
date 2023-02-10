# Namespacing-Swift-code-with-nested-types

```swift

struct Post {
    let id: Int
    let author: User
    let title: String
    let text: String
}

class PostTextFormatter {
    private let options: Set<PostTextFormatterOption>

    init(options: Set<PostTextFormatterOption>) {
        self.options = options
    }

    func formatTitle(for post: Post) -> String {
        return post.title.formatted(withOptions: options)
    }

    func formatText(for post: Post) -> String {
        return post.text.formatted(withOptions: options)
    }
}

enum PostTextFormatterOption {
    case highlightNames
    case highlightLinks
}


```

```swift
struct Post {
    class TextFormatter {
        enum Option {
            case highlightNames
            case highlightLinks
        }

        private let options: Set<Option>

        init(options: Set<Option>) {
            self.options = options
        }

        func formatTitle(for post: Post) -> String {
            return post.title.formatted(withOptions: options)
        }

        func formatText(for post: Post) -> String {
            return post.text.formatted(withOptions: options)
        }
    }

    let id: Int
    let author: User
    let title: String
    let text: String
}
```

```swift
struct Post {
    let id: Int
    let author: User
    let title: String
    let text: String

    // MARK: - TextFormatter
    
    class TextFormatter {
        private let options: Set<Option>

        init(options: Set<Option>) {
            self.options = options
        }

        func formatTitle(for post: Post) -> String {
            return post.title.formatted(withOptions: options)
        }

        func formatText(for post: Post) -> String {
            return post.text.formatted(withOptions: options)
        }

        // MARK: - Option
        
        enum Option {
            case highlightNames
            case highlightLinks
        }
    }
}
```

```swift
struct Post {
    let id: Int
    let author: User
    let title: String
    let text: String
}

extension Post {
    class TextFormatter {
        private let options: Set<Option>

        init(options: Set<Option>) {
            self.options = options
        }

        func formatTitle(for post: Post) -> String {
            return post.title.formatted(withOptions: options)
        }

        func formatText(for post: Post) -> String {
            return post.text.formatted(withOptions: options)
        }
    }
}

extension Post.TextFormatter {
    enum Option {
        case highlightNames
        case highlightLinks
    }
}
```

```swift
struct Post {
    typealias TextFormatter = PostTextFormatter

    let id: Int
    let author: User
    let title: String
    let text: String
}

class PostTextFormatter {
    typealias Option = PostTextFormatterOption

    private let options: Set<Option>

    init(options: Set<Option>) {
        self.options = options
    }

    func formatTitle(for post: Post) -> String {
        return post.title.formatted(withOptions: options)
    }

    func formatText(for post: Post) -> String {
        return post.text.formatted(withOptions: options)
    }
}

enum PostTextFormatterOption {
    case highlightNames
    case highlightLinks
}
```
