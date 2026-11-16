# FAQ

<details>

<summary>No music plays</summary>

xsound must run and start before lvl\_carplay. Check `Config.Audio.XSoundResource`.

</details>

<details>

<summary>GTA radio is silent</summary>

Another script turns the vehicle radio off (`SetVehRadioStation` to off or `SetUserRadioControlEnabled(false)`). Remove that from the other script.

</details>

<details>

<summary>Autopilot is missing</summary>

With `Config.Autopilot.Mode = 'models'` it shows only for the listed models. Use `'all'` for every car.

</details>

<details>

<summary>The lock button fights my keys script</summary>

Set `Config.Vehicle.Lock = false`.

</details>
