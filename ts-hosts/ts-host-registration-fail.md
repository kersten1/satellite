---

copyright:
  years: 2020, 2020
lastupdated: "2020-09-17"

keywords: satellite, hybrid, multicloud

subcollection: satellite

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Why does the host registration script fail?
{: #host-registration-script-fails}

{: tsSymptoms}
When you SSH into your own infrastructure machine that you want to add as a {{site.data.keyword.satelliteshort}} host and run the host registration script, you see a message similar to the following.
```
No package rh-python36 available.
Error: Nothing to do
```
{: screen}

{: tsCauses}
Your machine does not meet the minimum requirements to become a {{site.data.keyword.satelliteshort}} host. In particular, you must have the following packages installed on your RHEL 7 machine.
```
Repository 'rhel-ha-for-rhel-7-server-eus-rpms' is enabled for this system.
Repository 'rhel-server-rhscl-7-rpms' is enabled for this system.
Repository 'rhel-7-server-optional-rpms' is enabled for this system.
Repository 'rhel-7-server-eus-optional-rpms' is enabled for this system.
Repository 'rhel-7-server-rh-common-rpms' is enabled for this system.
Repository 'rhel-7-server-eus-rpms' is enabled for this system.
Repository 'rhel-ha-for-rhel-7-server-rpms' is enabled for this system.
Repository 'rhel-rs-for-rhel-7-server-eus-rpms' is enabled for this system.
Repository 'rhel-rs-for-rhel-7-server-rpms' is enabled for this system.
Repository 'rhel-7-server-rpms' is enabled for this system.
Repository 'rhel-7-server-supplementary-rpms' is enabled for this system.
Repository 'rhel-7-server-extras-rpms' is enabled for this system.
Repository 'rhel-7-server-eus-supplementary-rpms' is enabled for this system.
```
{: screen}

{: tsResolve}
1.  Add the required packages to your machine. For example, in IBM Cloud infrastructure you can run the following commands to add the required packages.
    1.  Refresh the Red Hat packages on your machine.
        ```
        subscription-manager refresh
        ```
        {: pre}

        If you see an error such as `Network error, unable to connect to server. Please see /var/log/rhsm/rhsm.log for more information.`, check the security group and other network settings for your machine to make sure that you have connectivity to the internet.
        {: tip}

    2.  Enable the package repositories on your machine.
        ```
        subscription-manager repos --enable=*
        ```
        {: pre}
2.  Make sure that your machine meets the other [host minimum requirements](/docs/satellite?topic=satellite-host-reqs), such as minimum CPU and memory sizes and public network connectivity.
3.  [Run the registration script](/docs/satellite?topic=satellite-hosts#add-hosts) on your machine again.