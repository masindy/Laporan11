<?php

namespace App\Controllers;

use App\Models\AsistenModel;

class AsistenController extends BaseController
{
    protected $asistenModel;
    public function __construct()
    {
        $this->asistenModel = new AsistenModel();
    }

    public function show()
    {
        $session = session();
        if ($session->has('username')) {
            $asisten = $this->asistenModel->findAll();
            $data = [
                'list' => $asisten
            ];
            return view('/asisten/AsistenView', $data);
        } else{
            return view('/asisten/Login');
        }
        
    }

    public function index()
    {
        $session = session();
        if ($session->has('username')) {
            return view('/asisten/AsistenView');
        } else{
            return view('/asisten/Login');
        }
        
    }

    public function simpan()
    {
        
        $session = session();
        if ($session->has('username')) {
            helper('form');
            // Memeriksa apakah melakukan submit data atau tidak.
            if (!$this->request->is('post')) {
                return view('/asisten/Simpan');
            }
            // Mengambil data yang disubmit dari form
            $post = $this->request->getPost([
                'nim', 'nama', "praktikum",
                "ipk"
            ]);
            // Mengakses Model untuk menyimpan data
            $model = model(AsistenModel::class);
            $model->simpan($post);
            return view('/asisten/Success');
        } else {
            return view('/asisten/Login');
        }    
    }

    public function edit()
    {
        $session = session();
        if ($session->has('username')) {
            $db = \Config\Database::connect();
            $builder = $db->table('asisten');
            helper('form');
            if (!$this->request->is('post')) {
                return view('/asisten/Update');
            }
            $data = [
                'nama' => [$this->request->getPost('nama')],
                'praktikum' => [$this->request->getPost('praktikum')],
                'ipk' => [$this->request->getPost('ipk')],
            ];
            $builder->where('nim', $this->request->getPost('nim'));
            $builder->update($data);

            return view('/asisten/Success');
        } else {
            return view('/asisten/Login');
        }
    }

    public function delete()
    {
        $session = session();
        if ($session->has('username')) {
            $db = \Config\Database::connect();
            $builder = $db->table('asisten');
            helper('form');
            if (!$this->request->is('post')) {
                return view('/asisten/Hapus');
            }
            $post = $this->request->getPost([
                'nim'
            ]);
            $builder->where('nim', $post);
            $builder->delete();
            return view('/asisten/Success');
        } else {
            return view('/asisten/Login');
        }
    }

    public function search()
    {
        $session = session();
        if ($session->has('username')) {
            if (!$this->request->is('post')) {
                return view('/asisten/search');
            }

            $nim = $this->request->getPost(['nim']);

            $model = model(AsistenModel::class);
            $asisten = $model->ambil($nim['nim']);

            $data = ['hasil' => $asisten];
            return view('/asisten/search', $data);
        } else {
            return view('/asisten/Login');
        }
    }

    public function login()
    {
        
        $post = $this->request->getPost(['usr', 'pwd']);
        $model = model(LoginAsisten::class);
        $user = $model->user(($post['usr']));
        $pwd = $model->user(($post['usr']));
        if ($user  && $pwd) {
            $session = session();
            $session->set('username', $post['usr']);
            $session->set('password', $post['pwd']);
            return view('/asisten/AsistenView');
        } else {
            return view('/asisten/login');
        }
    }
    public function logout()
    {
        $session = session();
        $session->destroy();
        return view('/asisten/Login');
    }
}
