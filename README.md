```html
private function convertToGoogleMap($data = null) {
        $arr = array();
        if (!is_null($data)) {

            foreach ($data as $a) {
                $_arr = ([$a['user']['firstname'].' '.$a['user']['lastname'], $a['latitude'], $a['longitude'], 1]);
                array_push($arr, $_arr);
            }
        }
        return json_encode($arr);
    }
```
