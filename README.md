# Server Side Hong Kong Siren Pack for FiveM

As this is an add-on, the vanilla siren hashes will not work automatically. You will need to edit your vehicle and ELS configuration files to use this custom siren pack correctly.

## Installation
1. Download the `.zip` file from the latest release.
2. Extract the folder to your server's `resources` directory.
3. Add `ensure hksirenpack` to your `server.cfg`.

## ELS-FiveM Configuration
Since this audio is an Add-On, standard native audio strings will not function. To use these sounds in your scripts, you must specify the custom audio string and ensure the audio bank is properly loaded.

### 1. Vehicle XML Configuration
For each vehicle you want to modify, follow these steps:

1. Open the `.xml` file that configures the vehicle's ELS.
2. Navigate to the `<SOUNDS>` element.
3. Edit the `AudioString` attribute for each tone to match the desired custom siren strings listed below.

**Original Example:**
```xml
<SOUNDS>
	<MainHorn InterruptsSiren="true" AudioString="SIRENS_AIRHORN" />
	<ManTone1 AllowUse="true" AudioString="VEHICLES_HORNS_SIREN_1" />
	<ManTone2 AllowUse="true" AudioString="VEHICLES_HORNS_SIREN_2" />
	<SrnTone1 AllowUse="true" AudioString="VEHICLES_HORNS_SIREN_1" />
	<SrnTone2 AllowUse="true" AudioString="VEHICLES_HORNS_SIREN_2" />
	<SrnTone3 AllowUse="true" AudioString="VEHICLES_HORNS_POLICE_WARNING" />
	<SrnTone4 AllowUse="true" AudioString="VEHICLES_HORNS_AMBULANCE_WARNING" />
	<AuxSiren AllowUse="true" AudioString="VEHICLES_HORNS_SIREN_1" />
	<PanicMde AllowUse="true" AudioString="VEHICLES_HORNS_POLICE_WARNING" />
</SOUNDS>
```

**Edited Example:**
```xml
<SOUNDS>
	<MainHorn InterruptsSiren="true" AudioString="ph7109_airhorn" />
	<ManTone1 AllowUse="true" AudioString="ph7109_wail" />
	<ManTone2 AllowUse="true" AudioString="ph7109_yelp" />
	<SrnTone1 AllowUse="true" AudioString="ph7109_wail" />
	<SrnTone2 AllowUse="true" AudioString="ph7109_yelp" />
	<SrnTone3 AllowUse="true" AudioString="ph7109_pulsar" />
	<SrnTone4 AllowUse="true" AudioString="ph7109_hilo" />
	<AuxSiren AllowUse="true" AudioString="ph7109_wail" />
	<PanicMde AllowUse="true" AudioString="ph7109_pulsar" />
</SOUNDS>
```

### 2. Lua Script Configuration
You also need to update the Lua script to load and play the custom audio bank.

1. Add the following line at the very top of `util.lua`:
   ```lua
   RequestScriptAudioBank('DLC_HKSIRENPACK\\SOUNDS', false)
   ```
2. Change the sound set for each `PlaySoundFromEntity` call in the script that plays the siren. You need to replace the default sound set (usually `0`) with `'HKSIRENPACK'`.

**From:**
```lua
PlaySoundFromEntity(h_soundID_veh[veh], getVehicleVCFInfo(veh).sounds.mainHorn.audioString, veh, 0, 0, 0)
```

**To:**
```lua
PlaySoundFromEntity(h_soundID_veh[veh], getVehicleVCFInfo(veh).sounds.mainHorn.audioString, veh, 'HKSIRENPACK', 0, 0)
```

## Other ELS Scripts
If you are using a different ELS script, you may need to consult the specific documentation provided by the author to find out how to change audio strings and sound banks. Here are a few common ones:

* **Tommy's ELS:** [Configuration Guide](https://tommys-scripts.gitbook.io/fivem/paid-scripts/tommys-els#configuration)
* **ScriptsM-ELS:** [Documentation](https://scriptsm-documentation.vercel.app/ScriptsM-ELS)

*(There are many custom ELS resources, it is impossible to list the instructions for all of them. The logic, however, remains similar to the steps above.)*

---

## Sound Set and Bank Configuration
When configuring, use the following:
- **Sound Set:** `HKSIRENPACK`
- **Sound Bank:** `dlc_hksirenpack/sounds`

## Available Sirens & Audio Strings
Below is the list of included siren boxes, the typical Hong Kong emergency vehicles they are used on, and their respective audio strings for script/meta usage.

### Premier Hazard 7109 (PH7109)
* **Usage:** A classic siren commonly heard on Hong Kong Fire Services Department (HKFSD) ambulances and various standard Hong Kong Police Force (HKPF) patrol vehicles.
* **Strings:**
  - `ph7109_airhorn`
  - `ph7109_wail`
  - `ph7109_yelp`
  - `ph7109_pulsar`
  - `ph7109_hilo`

### Haztec EuroMax 8-8110-2
* **Usage:** The standard siren frequently used by the Hong Kong Fire Services Department (HKFSD) for major fire appliances, pumpers, and hydraulic platforms.
* **Strings:**
  - `8-8110-2_airhorn`
  - `8-8110-2_a_wail`
  - `8-8110-2_a_yelp`
  - `8-8110-2_b_wail`
  - `8-8110-2_b_yelp`
  - `8-8110-2_pulsar`
  - `8-8110-2_hilo`

### Haztec EuroSmart 8-82613
* **Usage:** Found heavily on newer Hong Kong Police Force (HKPF), as well as several modern HKFSD command vehicles.
* **Strings:**
  - `8-82613_airhorn`
  - `8-82613_wail`
  - `8-82613_yelp`
  - `8-82613_pulsar`
  - `8-82613_hilo`

### Haztec EuroMax 8-8122 Series
* **Usage:** Commonly equipped on Hong Kong Police Force (HKPF) Traffic Branch vehicles and specialized units like the Police Tactical Unit (PTU) or Customs and Excise Department interceptors.
* **Strings:**
  - `8-8122_pl_airhorn` / `8-8122-2_pl_airhorn`
  - `8-8122_pl_wail` / `8-8122-2_pl_wail`
  - `8-8122_pl_yelp` / `8-8122-2_pl_yelp`
  - `8-8122_pl_pulsar` / `8-8122-2_pl_pulsar`
  - `8-8122_pl_hilo` / `8-8122-2_pl_hilo`

### Premier Hazard / ECCO 6009/6010
* **Usage:** Often found on older generation emergency vehicles, including traditional HKPF patrol cars, older fleet FSD appliances, and classic police motorcycles.
* **Strings:**
  - `ph6010_airhorn`
  - `ph6010_wail`
  - `ph6010_yelp`
  - `ph6010_pulsar`
  - `ph6010_hilo`

---

## Credits & Original Sources
A massive thank you to **[9032AP](https://www.lcpdfr.com/profile/475836-9032ap/)** on LSPDFR for providing the original siren audio files. This pack would not be possible without their high-quality recordings. 

Please check out and support their original audio mods here:
- [Haztec EuroSmart 8-82613](https://www.lcpdfr.com/downloads/gta5mods/audio/38879-haztec-eurosmart-8-82613/)
- [Haztec EuroMax 8-8110-2](https://www.lcpdfr.com/downloads/gta5mods/audio/37153-haztec-euromax-8-8110-2/)
- [Premier Hazard / ECCO 7109](https://www.lcpdfr.com/downloads/gta5mods/audio/33145-premier-hazard-ecco-7109/)
- [Haztec EuroMax 8-8122 Series](https://www.lcpdfr.com/downloads/gta5mods/audio/35496-haztec-euromax-8-8122-series/)
- [Premier Hazard / ECCO 6009/6010](https://www.lcpdfr.com/downloads/gta5mods/audio/38519-premier-hazard-ecco-60096010/)
This pack is a compilation of these individual siren mods, adapted for use in FiveM. Please support the original creator by downloading and endorsing their work on LSPDFR!

## End User Licence Agreement (EULA)
Original siren files are produced by 9032AP [https://www.lcpdfr.com/profile/475836-9032ap]. Current release is permitted and supported by 9032AP.You are allowed to host these as server-sided asset or as local files. No unauthorised online or offline redistribution of this mod pack is allowed unless permission is granted by both 9032AP and GaryLuk. By downloading the files, you agree to this EULA. Any unauthorised form of redistribution may face legal actions by 9032AP.
