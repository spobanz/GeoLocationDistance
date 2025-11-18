# GeoLocationDistance
function GeoLocationDistance(float $lat1, float $lon1, float $lat2, float $lon2): array
{
    $earthRadiusKm = 6371.0088;

    $lat1 = deg2rad($lat1);
    $lon1 = deg2rad($lon1);
    $lat2 = deg2rad($lat2);
    $lon2 = deg2rad($lon2);

    $latDelta = $lat2 - $lat1;
    $lonDelta = $lon2 - $lon1;

    $a = sin($latDelta / 2) ** 2 +
         cos($lat1) * cos($lat2) * sin($lonDelta / 2) ** 2;

    $c = 2 * atan2(sqrt($a), sqrt(1 - $a));

    $kilometers = $earthRadiusKm * $c;
    $miles = $kilometers * 0.621371;

    return [
        'kilometers' => $kilometers,
        'miles'      => $miles,
    ];
}
