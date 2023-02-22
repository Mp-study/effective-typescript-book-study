# Item 29: Be Liberal in What You Accept and Strict in What You Produce

## Liberal Type

Types that can accept in optionally,

```d
interface CameraOptions {
 center?: LngLat;
 zoom?: number;
 bearing?: number;
 pitch?: number;
}
```

```q
type LngLat =
 { lng: number; lat: number; } |
 { lon: number; lat: number; } |
 [number, number];

```

## Too much, libral typing will cause many type errors 😥

```d
function focusOnFeature(f: Feature) {
 const bounds = calculateBoundingBox(f);
 const camera = viewportForBounds(bounds);
 setCamera(camera);
 const {center: {lat, lng}, zoom} = camera;
 // ~~~ Property 'lat' does not exist on type ...
 // ~~~ Property 'lng' does not exist on type ...
 zoom; // Type is number | undefined
 window.location.search = `?v=@${lat},${lng}z${zoom}`;
}

```

## "Array and Array-like", "Omit and Partial" will help solving the problem like above 😀

```d
interface LngLat { lng: number; lat: number; };
type LngLatLike = LngLat | { lon: number; lat: number; } | [number, number];

interface Camera {
 center: LngLat;
 zoom: number;
 bearing: number;
 pitch: number;
}

interface CameraOptions extends Omit<Partial<Camera>, 'center'> {
 center?: LngLatLike;
}

type LngLatBounds =
 {northeast: LngLatLike, southwest: LngLatLike} |
 [LngLatLike, LngLatLike] |
 [number, number, number, number];

declare function setCamera(camera: CameraOptions): void;
declare function viewportForBounds(bounds: LngLatBounds): Camera;

```

## Resolved type errors 😆

```d
function focusOnFeature(f: Feature) {
 const bounds = calculateBoundingBox(f);
 const camera = viewportForBounds(bounds);
 setCamera(camera);
 const {center: {lat, lng}, zoom} = camera; // OK
 zoom; // Type is number
 window.location.search = `?v=@${lat},${lng}z${zoom}`;
}
```
