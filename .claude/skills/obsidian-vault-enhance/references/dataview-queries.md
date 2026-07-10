# Dataview Query Templates for Vault Notes

Reusable Dataview query templates. Adapt the `FROM` clause to target the correct folder.

## Course Schedule Table

**Use in**: Domain Index notes (e.g., RHCSA_00_Index.md).

```dataview
TABLE order AS "章", file.link AS "笔记", topic AS "内容概要"
FROM "20_Areas/21_RHEL/RHCSA"
WHERE order != null AND file.name != "RHCSA_00_Index"
SORT order ASC
```

Adapt for other folders:
```dataview
TABLE order AS "编号", file.link AS "笔记", topic AS "主题"
FROM "<folder-path>"
WHERE order != null AND file.name != "<index-filename>"
SORT order ASC
```

## Stub Notes Table

**Use in**: Domain Index notes to show `status: inbox` placeholders.

```dataview
TABLE topic AS "主题", file.mtime AS "最后修改"
FROM "20_Areas/21_RHEL"
WHERE status = "inbox"
SORT file.name ASC
```

## Tag Index

**Use in**: Domain Index notes for tag-based browsing.

```dataview
TABLE rows.file.link AS "笔记"
FROM "<folder-path>"
WHERE file.name != "<index-filename>"
FLATTEN tags AS tag
GROUP BY tag
SORT tag ASC
```

## Area Distribution (Dashboard)

**Use in**: Dashboard.md.

```dataview
TABLE rows.file.link AS "笔记"
FROM -"91_System" AND -"90_Archive"
GROUP BY split(file.folder, "/")[0] AS "区域"
```

## Status Statistics (Dashboard)

**Use in**: Dashboard.md.

```dataview
TABLE length(rows) AS "数量"
GROUP BY status AS "状态"
SORT status ASC
```

## Recent Updates (Dashboard)

**Use in**: Dashboard.md.

```dataview
TABLE updated AS "最后更新", file.link AS "笔记"
FROM ""
SORT updated DESC
LIMIT 10
```

## Orphan Notes (Dashboard)

**Use in**: Dashboard.md. Notes with zero incoming links.

```dataview
TABLE file.link AS "孤立笔记", file.mtime AS "最后修改"
FROM -"91_System" AND -"90_Archive" AND -"00_Inbox"
WHERE length(file.inlinks) = 0
SORT file.mtime DESC
```

## Full-Orphan Scan (All notes, no exclusions)

```dataview
TABLE file.link AS "笔记", file.mtime AS "最后修改"
WHERE length(file.inlinks) = 0 AND file.name != "Dashboard"
SORT file.mtime DESC
```

## Notes by Tag

```dataview
TABLE rows.file.link AS "笔记"
FROM -"91_System"
FLATTEN tags AS tag
GROUP BY tag
SORT tag ASC
```

## References

- [Dataview Documentation](https://blacksmithgu.github.io/obsidian-dataview/)
- [Dataview Query Types](https://blacksmithgu.github.io/obsidian-dataview/api/code-reference/)
- Obsidian Bases Skill _(not yet curated)_ — for `.base` file alternatives