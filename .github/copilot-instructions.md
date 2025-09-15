# Freestyle Expo - React Native Mobile App

Freestyle Expo is a React Native mobile application built with Expo that supports iOS, Android, and web platforms. The app uses Expo Router for file-based navigation, TypeScript for type safety, and includes modern React Native features like theming and animations.

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Bootstrap and Build
Run these commands in sequence to set up and build the project:

1. **Install dependencies**: `npm install` 
   - Takes approximately 34 seconds
   - Downloads ~946 packages including Expo SDK and React Native dependencies
   - May show deprecation warnings for some packages - these are normal

2. **Lint the code**: `npm run lint`
   - Takes approximately 2.5 seconds
   - Uses ESLint with expo-config-eslint configuration
   - Always run before committing changes

### Development Servers

**Start development server for all platforms:**
```bash
npx expo start
```
- NEVER CANCEL: Server startup takes 20-30 seconds. Set timeout to 60+ minutes.
- Runs on port 8081 by default
- Provides QR code for mobile testing (not available in CI environment)

**Start web development server:**
```bash
npm run dev
# OR
npx expo start --web --port 3000
```
- NEVER CANCEL: Web server startup takes 25-30 seconds. Set timeout to 60+ minutes.
- Accessible at http://localhost:3000
- Includes hot reloading for development

**Platform-specific development:**
```bash
npm run android    # Android emulator
npm run ios        # iOS simulator  
npm run web        # Web browser
```

### Production Build

**Export static web build:**
```bash
npx expo export --platform web
# OR for unminified development build:
npx expo export --platform web --no-minify
```
- NEVER CANCEL: Build takes 22-25 seconds. Set timeout to 60+ minutes.
- Outputs to `dist/` directory
- Generates static HTML files and bundled JavaScript
- Creates routes for: /, /explore, /_sitemap, /+not-found, /(tabs), /(tabs)/explore

## Validation

### Manual Validation Requirements
After making changes, ALWAYS perform these validation steps:

1. **Start the web development server** and verify it loads without errors
2. **Test navigation** by clicking between Home and Explore tabs
3. **Verify content rendering** on both pages:
   - Home page should show welcome message with steps
   - Explore page should show feature list with expandable items
4. **Check console** for any JavaScript errors or warnings
5. **Test responsive behavior** if making UI changes

### Validation Commands
Always run these commands before completing your work:
```bash
npm run lint          # Check code style (2.5 seconds)
npx expo export --platform web --no-minify  # Verify build works (22+ seconds)
```

### Expected Build Artifacts
After running export, verify these files exist in `dist/`:
```
dist/
├── index.html           # Home page
├── explore.html         # Explore page  
├── +not-found.html      # 404 page
├── _sitemap.html        # Sitemap
├── (tabs)/              # Tab layouts
├── _expo/               # Expo static assets
├── assets/              # Images and fonts
└── favicon.ico          # Site icon
```

## Project Structure

### Key Directories
```
/
├── app/                 # File-based routing (Expo Router)
│   ├── (tabs)/         # Tab navigation layout
│   │   ├── index.tsx   # Home screen
│   │   ├── explore.tsx # Explore screen
│   │   └── _layout.tsx # Tab layout configuration
│   ├── _layout.tsx     # Root layout with theming
│   └── +not-found.tsx  # 404 page
├── components/          # Reusable UI components
│   ├── ui/             # Platform-specific UI components
│   ├── ThemedText.tsx  # Text with theme support
│   ├── ThemedView.tsx  # View with theme support
│   └── ParallaxScrollView.tsx # Advanced scroll component
├── hooks/              # Custom React hooks
│   ├── useColorScheme.ts    # Light/dark mode detection
│   └── useThemeColor.ts     # Theme color management
├── constants/          # App configuration
│   └── Colors.ts       # Theme color definitions
├── assets/             # Static assets (images, fonts)
└── scripts/            # Build and utility scripts
    └── reset-project.js # Project reset utility
```

### Navigation System
- Uses **Expo Router** for file-based routing
- Tab navigation with Home and Explore screens
- Automatic deep linking support
- Type-safe navigation with TypeScript

### Theming System
- Light and dark mode support
- Automatic system theme detection
- Consistent color scheme across platforms
- Custom themed components (ThemedText, ThemedView)

## Common Tasks

### Adding New Screens
1. Create new `.tsx` file in `app/` directory
2. Export default React component
3. Navigation will be automatically configured based on file structure

### Modifying Existing Screens
- **Home screen**: Edit `app/(tabs)/index.tsx`
- **Explore screen**: Edit `app/(tabs)/explore.tsx`
- **Tab layout**: Edit `app/(tabs)/_layout.tsx`
- **Root layout**: Edit `app/_layout.tsx`

### Working with Components
- **Themed components**: Use `ThemedText` and `ThemedView` for consistent theming
- **Platform-specific**: Check `components/ui/` for iOS/Android specific implementations
- **Icons**: Use `IconSymbol` component for SF Symbols (iOS) and equivalent icons

### Styling Guidelines
- Use StyleSheet.create() for component styles
- Follow existing color scheme from `constants/Colors.ts`
- Test both light and dark themes
- Ensure cross-platform compatibility

## Configuration Files

### Key Configuration
- **package.json**: Scripts, dependencies, and project metadata
- **app.json**: Expo app configuration, icons, splash screen
- **tsconfig.json**: TypeScript configuration with path mapping
- **eslint.config.js**: Code linting rules

### Project Reset
Run `npm run reset-project` to move current app to `app-example/` and create blank app structure.

## Troubleshooting

### Common Issues
- **Port conflicts**: Use `--port 3000` flag or different port numbers
- **Metro bundler issues**: Clear cache with `npx expo start --clear`
- **TypeScript errors**: Ensure all imports use proper path aliases (`@/`)
- **Build failures**: Check for syntax errors and run `npm run lint`

### Environment Notes
- **CI mode**: Metro runs in CI mode in automated environments (no hot reloading)
- **Networking disabled**: Some Expo services unavailable in sandboxed environments
- **Offline mode**: Uses local dependency maps when network unavailable

### Performance
- Install time: ~34 seconds
- Lint time: ~2.5 seconds  
- Development server startup: 25-30 seconds
- Web build time: 22-25 seconds
- **NEVER CANCEL long-running commands** - they are normal for mobile development