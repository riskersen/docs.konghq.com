---
title: Install Kong Gateway on Ubuntu
---

The {{site.base_gateway}} software is governed by the
[Kong Software License Agreement](https://konghq.com/kongsoftwarelicense).
Kong is licensed under an
[Apache 2.0 license](https://github.com/Kong/kong/blob/master/LICENSE).

## Prerequisites

* A supported system with root or [root-equivalent](/gateway/{{page.kong_version}}/production/running-kong/kong-user) access.
* (Enterprise only) A `license.json` file from Kong

## Download and install

You can install {{site.base_gateway}} by downloading an installation package or using our APT repository.

{:.note .no-icon}
> We currently package {{ site.base_gateway }} for Ubuntu Bionic and Focal.
> If you are using a different release, replace `$(lsb_release -sc)` with `focal` in the commands below.
> <br /><br />
> To check your release name run `lsb_release -sc`.


{% navtabs %}
{% navtab Package %}

Install {{site.base_gateway}} on Ubuntu from the command line.

1. Download the Kong package:

{% capture download_package %}
{% navtabs_ee codeblock %}
{% navtab Kong Gateway %}
```bash
curl -Lo kong-enterprise-edition-{{page.versions.ee}}.all.deb "{{ site.links.download }}/gateway-3.x-ubuntu-$(lsb_release -sc)/pool/all/k/kong-enterprise-edition/kong-enterprise-edition_{{page.versions.ee}}_amd64.deb"
```
{% endnavtab %}
{% navtab Kong Gateway (OSS) %}
```bash
curl -Lo kong-{{page.versions.ce}}.amd64.deb "{{ site.links.download }}/gateway-3.x-ubuntu-$(lsb_release -sc)/pool/all/k/kong/kong_{{page.versions.ce}}_amd64.deb"
 ```
{% endnavtab %}
{% endnavtabs_ee %}
{% endcapture %}

{{ download_package | indent | replace: " </code>", "</code>" }}

2. Install the package:

{% capture install_package %}
{% navtabs_ee codeblock %}
{% navtab Kong Gateway %}
```bash
sudo dpkg -i kong-enterprise-edition-{{page.versions.ee}}.all.deb
```
{% endnavtab %}
{% navtab Kong Gateway (OSS) %}
```bash
sudo dpkg -i kong-{{page.versions.ce}}.amd64.deb
```
{% endnavtab %}
{% endnavtabs_ee %}
{% endcapture %}

{{ install_package | indent | replace: " </code>", "</code>" }}

3. (Optional) Prevent accidental upgrades by marking the package as `hold`:
{% capture optional %}
{% navtabs_ee %}
{% navtab Kong Gateway %}
```bash
sudo apt-mark hold kong-enterprise-edition
```
{% endnavtab %}
{% navtab Kong Gateway (OSS) %}
```bash
sudo apt-mark hold kong
```
{% endnavtab %}
{% endnavtabs_ee %}
{% endcapture %}
{{ optional | indent | replace: " </code>", "</code>" }}

{% navtabs_ee %}
{% navtab Kong Gateway %}
{:.note .no-icon}
> To uninstall the package, run: `sudo apt remove kong-enterprise-edition`.
{% endnavtab %}
{% navtab Kong Gateway (OSS) %}
{:.note .no-icon}
> To uninstall the package, run: `sudo apt remove kong`.
{% endnavtab %}
{% endnavtabs_ee %}

{% endnavtab %}
{% navtab APT repository %}

Install the APT repository from the command line.

1. Setup the Kong APT repository:
    ```bash
    echo "deb [trusted=yes] {{ site.links.download }}/gateway-3.x-ubuntu-$(lsb_release -sc)/ \
    default all" | sudo tee /etc/apt/sources.list.d/kong.list
    ```

2. Update the repository:
    ```bash
    sudo apt-get update
    ```

3. Install Kong:

{% capture install_from_repo %}
{% navtabs_ee codeblock %}
{% navtab Kong Gateway %}
```bash
sudo apt install -y kong-enterprise-edition={{page.versions.ee}}
```
{% endnavtab %}
{% navtab Kong Gateway (OSS) %}
```bash
apt install -y kong={{page.versions.ce}}
```
{% endnavtab %}
{% endnavtabs_ee %}
{% endcapture %}

{{ install_from_repo | indent | replace: " </code>", "</code>" }}

{% endnavtab %}
{% endnavtabs %}

{% include_cached /md/gateway/setup.md kong_version=page.kong_version %}


