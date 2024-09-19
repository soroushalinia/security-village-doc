# Introduction

This document provides a high-level explanation of the CMS API architecture and model relationships. For detailed API routes and documentation, please refer to the [Routes API Documentation](./routes/index.md).

## Overview

The CMS allows authors and site administrators to manage posts, tags, and images through a user-friendly API. The system is built with security in mind, ensuring everything including markdown content is sanitized and escaped properly before being exposed via the API. The CMS follows a markdown-based approach for post content with proper image handling and soft deletion mechanisms.
