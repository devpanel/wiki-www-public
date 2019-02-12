---
herotitle: 'Get in Touch'
herosubtitle: 'Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin.'
formimage: unicorn.svg
media_order: unicorn.svg
title: Contact
visible: false
body_classes: contact
access:
    site.login: true
    admin.login: true
forms:
    contact-form:
        classes: justify-content-center
        fields:
            -
                name: honeypot
                type: honeypot
            -
                name: name
                label: Name
                placeholder: 'Enter your name'
                type: text
                classes: form-control
                outerclasses: form-group
                validate:
                    required: true
            -
                name: email
                label: Email
                placeholder: 'Enter your email address'
                type: email
                classes: form-control
                outerclasses: form-group
                validate:
                    required: true
            -
                name: message
                label: Message
                placeholder: 'Enter your message'
                type: textarea
                rows: 4
                cols: 50
                classes: form-control
                outerclasses: form-group
                validate:
                    required: true
        buttons:
            -
                type: submit
                value: Send
                classes: 'btn btn-secondary ripple-out w-100'
        process:
            -
                save:
                    fileprefix: feedback-
                    dateformat: Ymd-His-u
                    extension: txt
                    body: '{% include ''forms/data.txt.twig'' %}'
            -
                email:
                    from:
                        mail: '{{ config.plugins.email.from }}'
                        name: 'devPanel Contact Form'
                    to:
                        mail: '{{ form.value.email }}'
                        name: '{{ form.value.name|e }}'
                    bcc: '{{ config.plugins.email.to }}'
                    reply_to: '{{ form.value.email }}'
                    subject: '[Contact Form] New message from {{ form.value.name|e }}'
                    body: '{% include ''forms/data.html.twig'' %}'
            -
                message: 'Thank you for your message! We will get back to you as soon as possible.'
            -
                display: thankyou
---

