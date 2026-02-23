# Collections

Collections are logical groupings of files in WROLPi. They organize related content together,
such as all videos from a channel or all archives from a domain.

## How Collections Work

Collections are tied to specific directories. All files within a collection's directory
automatically belong to that collection. When you download new content to that directory,
it's automatically included.

Examples:

- Video channels stored in `/media/wrolpi/videos/My Favorite Channel`
- Archives from a domain stored in `/media/wrolpi/archives/example.com`

> **A Collection cannot contain another Collection!**

## Collection Kinds

Collections are categorized by kind:

| Kind      | Purpose                            | Default Location             |
|-----------|------------------------------------|-----------------------------|
| `channel` | Video channels (YouTube, etc.)     | `/media/wrolpi/videos/`     |
| `domain`  | Website archives (SingleFile, etc.)| `/media/wrolpi/archives/`   |

## Automatic Collection Creation

WROLPi automatically creates collections in several scenarios:

- **Video downloads**: When downloading from a channel, WROLPi creates a channel collection
- **Archive downloads**: When archiving a website, WROLPi creates a domain collection

## Collection Properties

Each collection tracks:

- **Name**: The collection identifier (channel name, domain name, etc.)
- **Directory**: The directory containing the collection's files (must be unique)
- **Tag**: Optional tag for categorization and filtering
- **File Format**: The naming format used at last reorganization
- **Item Count**: Number of files in the collection
- **Total Size**: Combined size of all files

## Working with Collections

### Viewing Collections

Collections appear in several places:

- **Videos page**: Channel collections show in the Channels view
- **Archives page**: Domain collections show in the Domains view

### Collection Actions

From a collection page you can:

- **Download new content**: Add more videos/archives to the collection
- **Tag files**: Apply or remove tags from all items
- **Reorganize**: Move files to match a new naming format (see [Reorganization](reorganization.md))
- **Refresh**: Rescan the directory for new files

## Download Destinations

Download destinations are determined by two template settings:

### New Collections

When downloading from a new channel or domain, WROLPi creates a collection using the
**special directories template** from Settings. This determines where the collection's
directory is created:

- `videos_destination` - Template for new video channels
- `archive_destination` - Template for new archive domains

Example: If `videos_destination` is `%(name)s`, downloading from "Tech Channel" creates
the collection at `/media/wrolpi/videos/Tech Channel/`.

### Existing Collections

When downloading to an existing collection, files are placed within the collection's
directory using the **file format template**. This template controls how files are
named and organized within the collection:

```
%(upload_year)s/%(title)s.%(ext)s
```

Example: A video uploaded in 2024 titled "Tutorial" goes to
`/media/wrolpi/videos/Tech Channel/2024/Tutorial.mp4`.

### Template Variables

| Variable          | Description                        |
|-------------------|------------------------------------|
| `%(name)s`        | Collection name                    |
| `%(tag)s`         | Tag name (if tagged)               |
| `%(kind)s`        | Collection kind (channel/domain)   |
| `%(upload_year)s` | Year of upload (videos)            |
| `%(upload_month)s`| Month of upload (videos)           |
| `%(title)s`       | Video/archive title                |
| `%(ext)s`         | File extension                     |

## Related Documentation

- [Reorganization](reorganization.md) - Moving files to match new naming formats
- [Videos](../../modules/videos/index.md) - Video channel management
- [Archives](../../modules/archives/index.md) - Website archive management
