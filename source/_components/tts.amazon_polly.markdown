---
layout: page
title: "Amazon Polly"
description: "Instructions on how to setup Amazon Polly with Home Assistant."
date: 2017-01-28 09:00
sidebar: true
comments: false
sharing: true
footer: true
logo: polly.png
ha_category: Text-to-speech
ha_release: 0.37
---

The `amazon_polly` text-to-speech platform that works with [Amazon Polly](https://aws.amazon.com/polly/) to create the spoken output.
Polly is a paid service via Amazon Web Services.  There is a [free tier](https://aws.amazon.com/polly/pricing/) for the first 12 months and then a charge per million characters afterwards.

## {% linkable_title Configuration %}

To get started, add the following lines to your `configuration.yaml` (example for Amazon Polly):

```yaml
# Example configuration.yaml entry
tts:
  - platform: amazon_polly
    aws_access_key_id: AWS_ACCESS_KEY_ID
    aws_secret_access_key: AWS_SECRET_ACCESS_KEY
```

{% configuration %}
aws_access_key_id:
  description: "Your AWS Access Key ID. For more information, please read the [AWS General Reference regarding Security Credentials](http://docs.aws.amazon.com/general/latest/gr/aws-security-credentials.html). If provided, you must also provide an `aws_secret_access_key` and must **not** provide a `profile_name`."
  required: true
  type: string
aws_secret_access_key:
  description: "Your AWS Secret Access Key. For more information, please read the [AWS General Reference regarding Security Credentials](http://docs.aws.amazon.com/general/latest/gr/aws-security-credentials.html). If provided, you must also provide an `aws_access_key_id` and must **not** provide a `profile_name`."
  required: true
  type: string
profile_name:
  description: A credentials profile name. For more information, please see the [boto3 Documentation](http://boto3.readthedocs.io/en/latest/guide/configuration.html#shared-credentials-file) for more information.
  required: false
  type: string
region_name:
  description: "The region identifier to connect to. The default is `us-east-1`. See the [AWS Regions and Endpoints Reference](https://docs.aws.amazon.com/general/latest/gr/rande.html#pol_region) for available regions."
  required: false
  type: string or list
name:
  description: "Setting the optional parameter `name` allows multiple notifiers to be created. The default value is `notify`. The notifier will bind to the service `notify.NOTIFIER_NAME`."
  required: false
  type: string
text_type:
  description: "Specify wherever to use text (default) or ssml markup by default."
  required: false
  type: string
  default: text
voice:
  description: "Voice name to be used. See the [Amazon Documentation](http://docs.aws.amazon.com/polly/latest/dg/voicelist.html) for available voices."
  required: false
  type: string
output_format:
  description: "Override the default output format, e.g., `mp3`, `ogg_vorbis` or `pcm`."
  required: false
  type: string
  default: mp3
sample_rate:
  description: "Override the default sample rate, defaults to 22050 for MP3 and Ogg Vorbis, 16000 for pcm."
  required: false
  type: string
{% endconfiguration %}

 
## {% linkable_title Usage %}

Say to all `media_player` device entities:

```yaml
- service: tts.amazon_polly_say
  data_template:
    message: '<speak>Hello from Amazon Polly</speak>'
```

or

```yaml
- service: tts.amazon_polly_say
  data_template:
    message: >
      <speak>
          Hello from Amazon Polly
      </speak>
```

Say to the `media_player.living_room` device entity:

```yaml
- service: tts.amazon_polly_say
  data_template:
    entity_id: media_player.living_room
    message: >
      <speak>
          Hello from Amazon Polly
      </speak>
```

Say with break:

```yaml
- service: tts.amazon_polly_say
  data_template:
    message: >
      <speak>
          Hello from
          <break time=".9s" />
          Amazon Polly
      </speak>
```
