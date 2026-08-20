# Architecture — FitTrack (working name)

## Overview

Single React Native (Expo managed) app for iOS + Android. All data local:
SQLite via expo-sqlite holds users, workouts, and calorie entries. No
backend services in the MVP.

## Approved technology decisions

- Expo (managed workflow), TypeScript (DEC-1)
- expo-sqlite for persistence (DEC-2)
- Local-only auth: salted hash (expo-crypto), session held in memory +
  expo-secure-store for "stay signed in" (DEC-3)
- GitHub repo + kanban board; stories map 1:1 to issues (DEC-4)

## Components

- Auth module: registration, login, logout, session
- Data layer: SQLite schema + typed query functions (users, workouts, calorie_entries)
- Tracking screens: log a workout (type, duration, calories burned), log calories consumed
- Stats screen: totals/averages, history list with sorting (date, calories, duration, type)
- Navigation: auth stack vs. main tab stack

## Data model (high level)

users(id, username UNIQUE, password_hash, salt, created_at)
workouts(id, user_id FK, type, duration_min, calories_burned, performed_at)
calorie_entries(id, user_id FK, description, calories, consumed_at)

## Non-goals / explicitly out of scope (MVP)

Cloud sync, social features, wearables, notifications, real backend auth,
charts beyond simple lists/summaries (may be a fast-follow).
