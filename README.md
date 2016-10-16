```html
<?php

namespace App\Controller;

use App\Controller\AppController;
use Cake\Event\Event;
use Cake\ORM\TableRegistry; // Add this

class HomeController extends AppController {

    public function beforeFilter(Event $event) {
        parent::beforeFilter($event);
        $this->Auth->allow(['index']);
    }

    public function index() {
         $userModel = TableRegistry::get('Users'); // Add this
         
         $query = $userModel->find('all')
                 ->select(['firstname','lastname','latitude', 'longitude']);
         $map = $this->convertToGoogleMap($query->toArray());
         $this->set('map',$map);
    }
    
    private function convertToGoogleMap($data = null) {
        $arr = array();
        if (!is_null($data)) {

            foreach ($data as $a) {
                $_arr = ([$a['firstname'].' '.$a['lastname'], $a['latitude'], $a['longitude'], 1]);
                array_push($arr, $_arr);
            }
        }
        return json_encode($arr);
    }

}

```
