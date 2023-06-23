# PowerPanel (pwrstat) API 

This is a very simple REST API that wraps the PowerPanel pwrstat application for CyberPower battery backups. Only basic GET support for a single JSON object response for all parameters of the UPS are implemented.

# Usage

  - Clone GitHub repo to local computer.
  - Must have Linux PowerPanel application from CyberPower already downloaded (https://www.cyberpowersystems.com/product/software/powerpanel-for-linux/)
  - Place powerpanel_ver_amd64.deb OR PPL-*-64bit.deb (newer) file downloaded from above address in the folder containing this README, on your local computer.
  - Run Docker build, or use included Docker-Compose example. 
  - Note that you cannot use this GitHub repo as a Docker-Compose build context, due to needing to download a local copy of the CyberPower binary.
  - Access JSON response at http://<docker host IP>:5002/pwrstat

# Home Assistant

This is the template for Home Assistant, extracted from this Reddit [post](https://www.reddit.com/r/homeassistant/comments/7rfi6z/how_i_interfaced_my_150_cyberpower_ups_with_home/)

```yaml
sensor:
- platform : rest 
  resource: http://your-ip-address:5002/pwrstat 
  name: Battery Backup 
  value_template: '{{ value_json["State"] }}' 
  json_attributes:  
    - Remaining Runtime 
    - Load 
    - Power Supply by 
    - Last Power Event 
    - Test Result 
    - Utility Voltage 
    - Line Interaction 
    - Battery Capacity 
```
