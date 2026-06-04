## Versioning
We used path-based versioning (/v1/) because it provides explicit API lifecycle separation and avoids breaking changes for existing clients. It is also easier to manage in gateways and documentation systems compared to header-based versioning.

## Batch Ordering and Partial Failures
Batch responses are keyed by client-provided IDs to avoid reliance on array ordering. If one image is corrupted, that specific key returns an error object while other valid images are processed normally. This ensures partial success without blocking the entire batch request.

## Async Lifecycle
Async jobs follow this lifecycle: queued → running → done/failed. Results are retained for 24 hours after completion to support retries and debugging. After that, job metadata is purged to reduce storage overhead.