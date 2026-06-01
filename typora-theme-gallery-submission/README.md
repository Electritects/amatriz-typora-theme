# Typora Theme Gallery Submission Staging

This folder mirrors the files needed for a Typora Theme Gallery pull request.

## Files

- `_posts/theme/2026-06-01-amatriz.md` - staged gallery post.
- `thumbnails/amatriz.png` - 250x200 thumbnail for the gallery `thumbnails/` directory.
- `media/theme/amatriz/amatriz.css` - dark AMatriz theme CSS.
- `media/theme/amatriz/amatriz-print-white.css` - white-print AMatriz theme CSS.
- `media/theme/amatriz/amatriz-preview.png` - preview image referenced by the staged post.

## Before Opening the Pull Request

1. Fork `typora/theme.typora.io`.
2. Copy the staged files into matching paths in the fork.
3. Publish this project repository or a release ZIP.
4. Replace the placeholder `homepage` and `download` URLs in `_posts/theme/2026-06-01-amatriz.md`.
5. Test the copied CSS in Typora, then open the pull request.

The Typora gallery currently asks for a post in `_posts`, a listed thumbnail in `thumbnails`, local testing, and a pull request.
