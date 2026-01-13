# First Presented Gaps (FVG Storage) Indicator

A Pine Script indicator for TradingView that detects, stores, and displays the first Fair Value Gap (FVG) that occurs each trading day during the morning session. This indicator is particularly useful for traders who want to track historical FVGs beyond TradingView's free plan limitations.

## Features

- **Automatic FVG Detection**: Identifies the first Fair Value Gap that forms between 9:31 AM and 11:00 AM EST on the 1-minute timeframe
- **Historical Storage**: Stores up to 20 days of first presented gaps for supported symbols (MNQ, NQ, MES, ES)
- **Multi-Timeframe Support**: Works on any timeframe while always detecting gaps on the 1-minute chart
- **Visual Display**: 
  - Solid lines marking the top and bottom of each gap
  - Dashed, transparent midpoint lines for easy reference
  - Day labels (D0, D1, D2, etc.) indicating how many days back each gap occurred
- **Customizable Display**: Control how many days to display, line colors, and line width
- **Smart Labeling**: Labels stay visible at the right edge of your chart, positioned after the line endpoints

## What is a Fair Value Gap?

A Fair Value Gap (FVG) is a three-candle pattern where:
- **Bullish FVG**: The low of the current candle is above the high of the candle two bars ago
- **Bearish FVG**: The high of the current candle is below the low of the candle two bars ago

This indicator specifically looks for the **first** FVG that appears each day during the morning session (9:31 AM - 11:00 AM EST).

## Installation

1. Open TradingView and navigate to the Pine Editor
2. Copy the contents of `fvg_storage.pine`
3. Paste into the Pine Editor
4. Click "Save" and then "Add to Chart"

## Settings

### Settings Group
- **Timezone**: Select your timezone (default: America/New_York)
  - Options: America/New_York, Europe/London, UTC

### Display Group
- **Days to Display**: Number of historical gaps to show (1-20, default: 20)
- **Show Gaps**: Toggle to show/hide all gap lines and labels
- **Line Width**: Thickness of the gap boundary lines (1-5, default: 2)
- **Bullish Color**: Color for bullish (green) gaps (default: #008000)
- **Bearish Color**: Color for bearish (red) gaps (default: #B22222)

## How It Works

### Detection Window
The indicator only counts FVGs that form between **9:31 AM and 11:00 AM EST** (excluding the 9:30 AM candle itself). This ensures you're tracking the first meaningful gap of the trading day.

### Historical Storage
- **Supported Symbols**: The indicator stores historical data for:
  - MNQ (Micro E-mini Nasdaq-100)
  - NQ (E-mini Nasdaq-100)
  - MES (Micro E-mini S&P 500)
  - ES (E-mini S&P 500)
- **Other Symbols**: For symbols not in the list above, the indicator will still display current gaps but won't store historical data
- **Storage Limit**: Up to 20 days of gaps are stored, with the oldest being removed when the limit is reached

### Day Labels
- **D0**: Today's first presented gap
- **D1**: Yesterday's gap
- **D2**: Two days ago
- And so on...

Labels are positioned to the right of the line endpoints and remain visible at the right edge of your chart as you scroll.

### Visual Elements
- **Top/Bottom Lines**: Solid lines marking the high and low boundaries of each gap
- **Midpoint Lines**: Dashed, semi-transparent lines showing the center of each gap
  - Light green for bullish gaps
  - Light pink for bearish gaps
- **Labels**: Day indicators (D0, D1, etc.) positioned after the line endpoints

## Usage Tips

1. **Best Timeframe**: While the indicator works on any timeframe, it's most useful on:
   - 1-minute charts for real-time gap detection
   - 5-minute or 15-minute charts for a broader view of historical gaps

2. **Historical Context**: Use the stored gaps to identify:
   - Support/resistance levels from previous days
   - Areas where price may react
   - Patterns in gap formation

3. **Display Management**: Adjust "Days to Display" based on your needs:
   - Lower values (5-10) for cleaner charts
   - Higher values (15-20) for more historical context

## Technical Details

- **Pine Script Version**: v6
- **Max Lines**: 500
- **Max Labels**: 500
- **Detection Timeframe**: Always uses 1-minute data via `request.security()`
- **Storage Method**: Arrays with automatic cleanup of oldest entries
- **Update Frequency**: Labels update on every bar to maintain sticky positioning

## Limitations

- Historical storage is limited to 20 days
- Only stores data for MNQ, NQ, MES, and ES symbols
- Detection window is fixed at 9:31 AM - 11:00 AM EST
- Requires TradingView account (free plan works, but historical data access is limited)

## Troubleshooting

**Gaps not appearing?**
- Ensure you're viewing a chart with 1-minute data available
- Check that the timezone setting matches your trading session
- Verify that gaps are forming during the 9:31 AM - 11:00 AM window

**Labels overlapping?**
- Reduce the "Days to Display" setting
- Adjust line width if lines are too thick

**Historical gaps missing?**
- Historical storage only works for MNQ, NQ, MES, and ES
- The indicator needs to have been running when those gaps formed
- TradingView's free plan may limit how far back you can see historical data

## License

This indicator is provided as-is for educational and trading purposes.
