# RH Customization Notes

This document records all customizations made to the InsightsLM codebase.

## Branding Changes (Date: 2025-08-09)

### Overview
Changed all occurrences of "InsightsLM" to "DaVinciNotes" across the web application frontend.

### Files Modified

#### 1. `index.html`
- **Line 7**: Updated page title from "InsightsLM" to "DaVinciNotes"
- **Line 11**: Updated OpenGraph title meta tag from "InsightsLM" to "DaVinciNotes"

#### 2. `src/pages/Auth.tsx`
- **Line 11**: Updated main heading from "InsightsLM" to "DaVinciNotes"

#### 3. `src/pages/Dashboard.tsx`
- **Lines 21, 39, 62, 80**: Updated "Welcome to InsightsLM" to "Welcome to DaVinciNotes" (4 occurrences)
- **Line 102**: Updated main welcome heading to "Welcome to DaVinciNotes"

#### 4. `src/components/dashboard/DashboardHeader.tsx`
- **Line 21**: Updated header title from "InsightsLM" to "DaVinciNotes"

#### 5. `src/components/dashboard/EmptyDashboard.tsx`
- **Line 31**: Updated description text from "InsightsLM is an AI-powered..." to "DaVinciNotes is an AI-powered..."

#### 6. `src/components/notebook/AddSourcesDialog.tsx`
- **Line 414**: Updated dialog title from "InsightsLM" to "DaVinciNotes"
- **Line 422**: Updated help text from "Sources let InsightsLM base..." to "Sources let DaVinciNotes base..."

#### 7. `src/components/notebook/ChatArea.tsx`
- **Line 308**: Updated footer disclaimer from "InsightsLM can be inaccurate..." to "DaVinciNotes can be inaccurate..."

#### 8. `supabase/migrations/20250606152423_v0.1.sql`
- **Line 3**: Updated database schema comment from "InsightsLM application" to "DaVinciNotes application"

### Impact
- Browser tab title now displays "DaVinciNotes"
- All user-facing text and headings reference "DaVinciNotes" instead of "InsightsLM"
- Consistent branding throughout the application interface

### Notes
- Backend files (N8N workflows, database migrations) were not modified to maintain functionality
- Only frontend user-facing text was updated
- Application functionality remains unchanged, only branding was modified

---

## Future Customizations
(Add new customizations below this section)