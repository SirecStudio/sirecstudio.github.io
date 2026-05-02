# SS-IdentityCard V4.5

## Update Summary

This is a major update for SS-IdentityCard. It introduces new integration support, UI optimizations, complete README documentation, and expanded translation coverage.

Please review the changes before updating, especially if your server uses archives, fines, or external job systems.

***

## Added

* Added integration support for `SS-CommunityJobs`.
* Added support for forced labor workflows for players with active dossiers from `SS-Archives`.
* Added fine repayment while working.
* Added complete README documentation with installation, configuration, and usage instructions.
* Added multiple language options: `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, and `PT`.

***

## SS-CommunityJobs Integration

`SS-CommunityJobs` integration has been added in preparation for the upcoming community jobs system.

Players can now perform different jobs, including forced labor for characters who have active dossiers from `SS-Archives`.

When a player is assigned to forced labor:

* The player does not receive normal payment.
* Their fines decrease gradually while working.
* Once all fines are cleared, the player starts receiving normal payment again.

***

## UI Optimizations

* Optimized the UI for better performance.
* Cleaned up the UI code structure.
* Improved maintainability for future updates.

***

## Documentation

* Added a complete README for SS-IdentityCard.
* The README includes detailed instructions for installation, configuration, and full feature usage.

***

## Config & Translations

* Added translation support for multiple languages.
* Included language options: `EN`, `RO`, `IT`, `DE`, `FR`, `ES`, and `PT`.
