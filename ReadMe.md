<p align="center">
  <a href="https://github.com/dibosh/kustron">
    <img alt="Kustron" title="Kustron" src="https://i.imgur.com/Nndv5Vv.png" width="300">
  </a>
</p>

<p align="center">
  Kustomize based kubernetes manifest generator. Simple but glorified!
</p>

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Usage](#usage)
- [Structure](#structure)
- [Feedback](#feedback)

## Introduction

If you have started moving your services to `kubernetes` cluster and was looking for a way to know how to write manifest files in a manageable and idiomatic way- `kustron` is for you. `kustron` is a simple cli tool that helps you generate manifest files for your service. `kustron` uses [kustomization](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/) and even generates `dockerfile` for your service specific language.

**Even though some of the manifest files are mainly targeted if you are using GKE(google kubernetes engine) but most of them are easily applicable for any other cloud providers.**

## Features

A few of the things `kustron` does for you:

* Generates k8s manifests with different env specific overrides
* Generates `dockerfile` for your specific stack; currently supported- `java spring boot`, `golang` and `nodejs`
* Generates a `Makefile` with helper commands that you can utilise in your CI/CD pipelines

## Usage

- Install via [npm](https://www.npmjs.com/)- `npm i -g kustron`

- In your service source dir, you can run this- `kustron -g` e.g. `cd projects/checkout-service && kustron -g`

- It will ask you a few questions regarding your app/service

- Once you have provided all the answers, a `deployment` folder will be generated with all the necessary files

- A `dockerfile` and `Makefile` will also be generated at the project root

- You can also do- `kustron -g -p /absolute/path/of/your/service/folder` to generate all the mentioned files and folders in the path you specified. e.g. `kustron -g /users/lbm/projects/gaan-recorder/`

- You can always do- `kustron -h` to check the help

## Structure

- The generated `deployment` folder will have following structure

```
- deployment
  - base
    - config
      - configmap.yml
      - hpa.yml
    - deployment.yml
    - ...
    - kustomization.yml
  - overrides
    - dev
      - ...
    - stg
      - ...
    - prd
      - ...
```

- `base` folder contains base configurations

- `overrides` folder has specific overrides, it considers you will deploy your service at least into 3 envs(e.g. `dev`, `stg`, `prd`)

- All the files have necessary comments to help you out with any modifications you want

- Adding another `env` override should be as simple as creating a dir under `overrides` and copying the files from any of the existing `env` and doing necessary amendments

- The goal is to get you started with your manifestation- but be mindful that whatever the modifications or additions you made, double check the `Makefile` to verify, if you have to make any amendments there too- in most of the cases, you won't need

## Feedback

Feel free to [file an issue](https://github.com/dibosh/kustron/issues/new).

Would love to extend this for other cloud providers and language options. Feel free to create a PR with one if you want to add. 


