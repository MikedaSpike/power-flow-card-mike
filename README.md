# Power Flow Card Mike (Dual Battery Fork)

![Latest Release](https://img.shields.io/github/v/release/MikedaSpike/power-flow-card-mike)
![Downloads](https://img.shields.io/github/downloads/MikedaSpike/power-flow-card-mike/total)
![License](https://img.shields.io/github/license/MikedaSpike/power-flow-card-mike)
![Issues](https://img.shields.io/github/issues/MikedaSpike/power-flow-card-mike)
![Last Commit](https://img.shields.io/github/last-commit/MikedaSpike/power-flow-card-mike)
![Commit Activity](https://img.shields.io/github/commit-activity/m/MikedaSpike/power-flow-card-mike)
![Stars](https://img.shields.io/github/stars/MikedaSpike/power-flow-card-mike)

---

## Table of Contents
- [About this Project](#about-this-project)
- [Preview](#preview)
- [Installation (Manual)](#installation-manual)
  - [Configuration Options](#configuration-options)
  - [Example Configuration](#example-configuration)
- [Development / Compiling from Source](#development--compiling-from-source)
- [Credits](#credits)
- [License](#license)

---
  
## About this Project
This is a maintained fork of the original [Power Flow Card](https://github.com/ulic75/power-flow-card). 

**Important Notice:** The original project has been archived and is no longer being updated. This version is specifically redesigned for users who have a solar setup with **exactly two batteries**. It does not support single-battery setups or systems with more than two.

## Preview
Here is how the card looks in a configuration with two batteries:

<img width="486" height="455" alt="Powerflow" src="https://github.com/user-attachments/assets/0e3aa08f-4848-4b7f-a0d1-567e3cae45ea" />


## Installation (Manual)
Since this version is optimized for a dual-battery setup, it is available as a manual install:

1. Download the latest `power-flow-card-mike.js` from the [Releases page](https://github.com/MikedaSpike/power-flow-card-mike/releases).
2. Copy the file into your Home Assistant `config/www/` directory.
3. Add the resource reference in Home Assistant:
   - Go to **Settings** > **Dashboards**.
   - Click the three-dot menu icon (top right) -> **Resources**.
   - Click **+ ADD RESOURCE**.
   - URL: `/local/power-flow-card-mike.js`
   - Resource type: `JavaScript Module`.

### Configuration Options

You can customize the card using the following options in your YAML dashboard configuration.

| Name | Type | Description |
| --- | --- | --- |
| `type` | `string` | Must be `custom:power-flow-card-mike`. |
| `title` | `string` | Optional: Shows a title at the top of the card. |
| `watt_threshold` | `number` | The number of watts to display before converting to kilowatts. Set to 0 to always display in kW. |
| `entities` | `object` | The container for all your sensor entities. |

#### Entities Configuration

At least one energy source (grid, battery, or solar) is required.

| Entity Key | Type | Description |
| --- | --- | --- |
| `grid` | `object` | Split object with `consumption` and `production` entities. |
| `solar` | `string` | Entity ID for your solar power production. |
| `battery` | `object` | First battery: split object with `consumption` and `production`. |
| `battery_charge` | `string` | Charge percentage entity for the first battery. |
| `battery2` | `object` | **Fork specific:** Second battery: split object with `consumption` and `production`. |
| `battery2_charge` | `string` | **Fork specific:** Charge percentage entity for the second battery. |
| `gas` | `string` | Entity ID for gas consumption. |
| `water` | `string` | Entity ID for water consumption. |

---

### Example Configuration

This example shows the full configuration with two batteries, solar, grid, gas, and water usage:

```yaml
type: custom:power-flow-card-mike
title: "Totaal:"
watt_threshold: 1000
entities:
  grid:
    consumption: sensor.daily_energy_consumption_w_converted
    production: sensor.daily_energy_delivery_w_converted
  solar: sensor.envoy_today_energy_production_w_converted
  
  # First Battery
  battery:
    consumption: sensor.marstek_m1_daily_discharging_energy
    production: sensor.marstek_m1_daily_charging_energy
  battery_charge: sensor.marstek_m1_percentage
  
  # Second Battery (Fork specific)
  battery2:
    consumption: sensor.marstek_m2_daily_discharging_energy
    production: sensor.marstek_m2_charging_energy
  battery2_charge: sensor.marstek_m2_percentage
  
  # Utilities
  gas: sensor.daily_gas_usage
  water: sensor.water_usage_sensor

```
## Development / Compiling from Source

If you want to modify the code and compile the custom card yourself, you will need to have [Node.js](https://nodejs.org/) installed on your computer.

1. **Download the source code:** Clone this repository using git, or download the ZIP file from GitHub and extract it to a folder.
2. **Open your terminal:** Navigate to the root folder of the downloaded project.
3. **Install dependencies (One-time setup):**
   Run the following command to download all required packages. You only need to do this once.
   ```bash
   npm install

## Credits

Based on the original [Power Flow Card](https://github.com/ulic75/power-flow-card). All credits for the design and base logic go to the original author and the [Home Assistant](https://www.home-assistant.io/) team.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

```
