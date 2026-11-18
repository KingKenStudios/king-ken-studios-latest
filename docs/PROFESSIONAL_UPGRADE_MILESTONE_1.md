# King Ken Studios — Professional Upgrade Milestone 1

## Scope completed in this milestone

This milestone establishes a shared visual foundation and makes a first functional improvement in the Photo Studio. It is intentionally incremental: the existing React/Vite, Express, Electron, SQLite, Zustand, and project-service architecture has not been replaced.

### Shared workstation design foundation

- Added shared King Ken Studios design tokens for graphite surfaces, borders, typography, amber action accents, red recording/destructive states, and panel treatments.
- Improved global focus visibility, selection styling, scrollbars, range-input accents, and reduced-motion handling.
- Increased the main studio shell header height and refined its graphite/border treatment.
- Updated the sidebar identity from `AIOS STUDIOS` to `CREATIVE SUITE` so King Ken Studios remains clearly identified as the creative application.
- Refined sidebar active navigation to use the warm amber selection treatment.
- Updated the global assistant launch label to `ANNY`.
- Removed the unsupported hardcoded `32-bit float` status label and replaced it with the neutral `Audio Engine` label.
- Added workspace-scoped styling hooks for Recording, Beat, Video, and Photo workspaces without changing their engine/service contracts.

### Security hardening started

- Public self-registration no longer accepts or grants the `Admin` role. New public accounts default to `User`; the explicitly selected `Creator` role remains available.
- Removed predictable hardcoded JWT signing and refresh secrets. Development now uses process-local random secrets; production fails closed unless independent environment secrets of at least 32 characters are configured.
- Added JWT secret configuration guidance to `.env.example`.
- Replaced Electron filesystem IPC string-prefix checks with path-relative boundary checks and real-path validation for reads, writes, deletes, directory creation, and existence checks. Added safe ancestor validation before recursive directory creation.

### Photo Studio functional improvement

- Added a real browser-canvas export path for PNG and JPEG.
- Export uses the current supported CSS color/filter look, source image dimensions, and JPEG quality setting.
- Replaced misleading TIFF/16-bit/transparent-cutout export options with the formats actually implemented by this browser export path.
- Corrected imported-file metadata so the interface no longer claims every imported image is a 16-bit RAW file.
- Clarified the ANNY image action: the current local action applies a built-in color look; prompt-driven neural image editing still requires a connected image model. The UI no longer claims facial-keypoint analysis or neural frequency separation is running when it is not.

## Files changed

- `src/index.css`
- `src/components/Layout.tsx`
- `src/components/Sidebar.tsx`
- `src/pages/RecordingStudio.tsx`
- `src/pages/BeatGenerator.tsx`
- `src/pages/VideoStudio.tsx`
- `src/pages/PhotoStudio.tsx`
- `server/config/jwt.ts` (new)
- `server/controllers/auth.controller.ts`
- `server/middleware/auth.ts`
- `electron/main.ts`
- `.env.example`

## Preservation notes

- No project database, user media, project format, server route, audio engine, video engine, or Electron process was intentionally replaced.
- No large studio page was rewritten in this milestone.
- The root application remains the source of truth; secondary frontend/mockup directories remain reference material only.

## Verification status

- Source archive extracted successfully.
- Targeted source edits and searches completed.
- Dependency installation (`npm ci`) did not complete within the execution window; the working environment therefore does not have a complete dependency tree.
- TypeScript/build verification could not be completed because the required package/type dependencies are unavailable. This milestone must not be described as production-build verified.
- The PNG/JPEG export should be exercised in the target browser with both a local imported image and a CORS-permitted remote image before release.

## Next milestones

1. Establish a clean dependency install and baseline build/typecheck.
2. Add automated tests for public registration role restrictions, JWT production configuration, and Electron path-boundary/symlink cases.
3. Replace remaining simulated or misleading UI actions with verified behavior or explicit unavailable/preview states.
4. Rebuild the recording and beat workspace layouts around clear beginner/advanced modes while retaining their existing engines.
5. Rebuild the video timeline and inspector workflow with professional editing affordances and verified media operations.
6. Expand Photo Studio into a non-destructive layer/mask editing workflow; do not claim unsupported RAW/16-bit processing until implemented.
7. Introduce real project templates that create validated project state, rather than static template cards or decorative usage metrics.
8. Add regression tests and benchmark performance on the supported desktop/web targets.
