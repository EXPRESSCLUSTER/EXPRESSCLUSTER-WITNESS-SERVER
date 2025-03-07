# EXPRESSCLUSTER Witness Server Setup

## Overview
This repository contains a step-by-step Quick Start Guide (QSG) for setting up a Witness Server in an existing EXPRESSCLUSTER environment. The Witness Server helps in maintaining quorum and improving high availability in a two-node cluster setup.

## Prerequisites
Before setting up the Witness Server, ensure that:
- You meet the [system requirements](https://docs.nec.co.jp/software/clustering/expresscluster_x/x52/ecx_x52_windows_en/W52_SG_EN/W_SG.html#system-requirements-for-the-witness-server).
- You have a Windows Server ready for installation.
- You have administrative privileges.

## Installation Steps

### 1. Install Node.js
Download and install **Node.js 18.13.0 or 20.10.0** from the official [Node.js website](https://nodejs.org/en/download).

### 2. Install the Required NPM Package
Obtain the Witness Server package (`clpwitnessd-<version>.tgz`) from the EXPRESSCLUSTER installation media:  

