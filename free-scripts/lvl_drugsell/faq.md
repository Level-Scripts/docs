# FAQ

<details>

<summary>"You have no drugs to sell" but I have them</summary>

The item name must be a key in `Config.Drugs`, and the item metadata must match one of its variants. A variant with `metadata = nil` only takes items without metadata.

</details>

<details>

<summary>Nothing happens on police calls</summary>

`Config.Dispatch` uses cd\_dispatch by default. Put the export or event of your dispatch script there.

</details>
