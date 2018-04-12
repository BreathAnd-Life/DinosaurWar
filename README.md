# DinosaurWar

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EnemyControl :MonoBehaviour
{
	private Rigidbody rBody;
	private Animator ani;
	private Transform player;//玩家的位置

	void Start()
	{
		rBody = GetComponent<Rigidbody> ();
		ani = GetComponent<Animation> ();
		player = GameObject.FindWithTag ("Player").transform; //按照给玩家对象设置的Tag名传进来
	}

	void Update()
	{
		if (player == null)
		{
			return;
		}
		//计算和玩家的距离
		float dis = Vector3.Distance (transform.position, player.position);
		if (dis < 2f) {
			//杀死玩家
			Destroy (player.gameObject);
			//播放站立（默认）动画
			ani.Play ("idle");
		} else if (dis < 5f) {
			//朝向玩家
			transform.LookAt (player.position);
			//追击玩家(乘以的速度倍速最好不要超过玩家的速度)
			rBody.velocity = transform.forward * 2;
			//播放跑步动画
			ani.Play ("Move");
		} 
		else
		{
			//待机状态
			ani.Play ("idle");
		}
	}

}	
