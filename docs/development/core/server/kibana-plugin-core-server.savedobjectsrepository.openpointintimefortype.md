<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [kibana-plugin-core-server](./kibana-plugin-core-server.md) &gt; [SavedObjectsRepository](./kibana-plugin-core-server.savedobjectsrepository.md) &gt; [openPointInTimeForType](./kibana-plugin-core-server.savedobjectsrepository.openpointintimefortype.md)

## SavedObjectsRepository.openPointInTimeForType() method

Opens a Point In Time (PIT) against the indices for the specified Saved Object types. The returned `id` can then be passed to `SavedObjects.find` to search against that PIT.

<b>Signature:</b>

```typescript
openPointInTimeForType(type: string | string[], { keepAlive, preference }?: SavedObjectsOpenPointInTimeOptions): Promise<SavedObjectsOpenPointInTimeResponse>;
```

## Parameters

|  Parameter | Type | Description |
|  --- | --- | --- |
|  type | <code>string &#124; string[]</code> |  |
|  { keepAlive, preference } | <code>SavedObjectsOpenPointInTimeOptions</code> |  |

<b>Returns:</b>

`Promise<SavedObjectsOpenPointInTimeResponse>`

{<!-- -->promise<!-- -->} - { id: string }

## Example


```ts
const repository = coreStart.savedObjects.createInternalRepository();

const { id } = await repository.openPointInTimeForType(
  type: 'index-pattern',
  { keepAlive: '2m' },
);
const page1 = await savedObjectsClient.find({
  type: 'visualization',
  sortField: 'updated_at',
  sortOrder: 'asc',
  pit,
});

const lastHit = page1.saved_objects[page1.saved_objects.length - 1];
const page2 = await savedObjectsClient.find({
  type: 'visualization',
  sortField: 'updated_at',
  sortOrder: 'asc',
  pit: { id: page1.pit_id },
  searchAfter: lastHit.sort,
});

await savedObjectsClient.closePointInTime(page2.pit_id);

```

