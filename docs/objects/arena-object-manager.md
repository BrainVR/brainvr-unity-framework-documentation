# Description

# Functions
## GetObject
`public ArenaObject GetObject(int i)`

Returns an object in the list if it exists at that particular index. Otherwise returns null.

## Show
`public void Show(int i)`

Calls [`Show`](arena-object.md#show) on object at that particular index if it exists.

## ShowAll
`public void ShowAll(bool bo = true)`

Iterates thorugh all objects and calls `Show(bo)` at each controller. See [Show](arena-object.md#show).

## Hide
`public void Show(int i)`

Calls [`Hide`](arena-object.md#hide) on object at that particular index if it exists.

## HideAll
`public void HideAll()`

Same as `ShowAll(false)`. Runs Hide on all arena object controllers. See [Hide](arena-object.md#hide).

## SetColor
`void SetColor(Color color)`

Sets colour of each obejct material if possible. See [SetColor](arena-object.md#setcolor).

## SetType
`void SetType(string s, bool force = false)`¨

Iterates though objects and sets each object ot appropriate type as possible. See [SetType](arena-object.md#settype).