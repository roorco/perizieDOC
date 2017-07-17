---
title: Contatti
form:
    name: contact-form
    fields:
        - name: name
          label: Nome e Cognome
          size: x-small
          type: text
          validate:
            required: true

        - name: email
          label: Email
          size: medium
          placeholder:
          type: email
          validate:
            required: true

        - name: message
          label: Messaggio
          size: large
          type: textarea
          validate:
            required: true

        - name: file
          type: file
          size: x-small
          multiple: false
          destination: '@self'
          accept:
            -image/*

    buttons:
        - type: submit
          value: Invia
        - type: reset
          value: Cancella

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Grazie
        - display: Grazie, La contatteremo al più presto

---

#Contatti
Compila i campi qui sotto o contattaci su info@periziedoc.com
