---
name: improve-stat432-plots
description: Improve the formatting of plots for STAT 432 homework in R or Python. Use this skill only when the user explicitly asks to use it.
---

# Improve STAT 432 Plots

Improve the appearance and readability of a plot without changing its data or statistical results.

## Formatting rules

- Use enough margins so that titles, labels, and legends are not cut off.
- Add a short and informative title.
- Label both axes clearly.
- Use readable tick labels and suitable axis limits.
- Use clear, colorblind-friendly colors.
- Use different symbols or line types for multiple curves.
- Keep grid lines light and inside the plotting panel.
- Place the legend inside an unused part of the plotting panel.
- Do not add a legend title unless the user explicitly requests one.
- Make sure all legend labels are fully visible.
- Do not change the data, statistical calculations, or conclusions.

## Layout and clipping checks

- Keep grid lines inside the plotting panel. In base R, draw grid lines with clipping enabled (`xpd = FALSE`).
- Do not set `xpd = NA` globally. Use it only while drawing an element that must appear outside the plotting panel, such as an external legend.
- Prefer placing the legend inside an unused part of the plotting panel.
- If the legend must be outside the panel, increase the appropriate figure margin and make sure the figure is wide enough.
- Use a smaller legend text size or shorter labels only when necessary. Do not allow legend text to be cut off.
- After producing the plot, inspect the rendered output and confirm that the title, axes, tick labels, grid lines, and complete legend are visible.
- Restore any changed graphical parameters after creating the plot.