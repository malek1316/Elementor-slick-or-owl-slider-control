# Elementor-slick-or-owl-slider-control
This is a elementor widget slider js run and developed control.

<?php
namespace Chariton\Widgets;

use Elementor\Widget_Base;
use Elementor\Controls_Manager;
use Elementor\Group_Control_Image_Size;
use Elementor\Group_Control_Typography;
use Elementor\Utils;


if ( ! defined( 'ABSPATH' ) ) exit; // Exit if accessed directly

/**
 * Elementor Style for header
 *
 *
 * @since 1.0.0
 */

class Testimonial extends Widget_Base {   //this name is added to plugin.php of the root folder

	public function get_name() {
		return 'section-testimonial';
	}

	public function get_title() {
		return 'Testimonial';   // title to show on elementor
	}

	public function get_icon() {
		return 'fal fa-quote-left';    //   eicon-posts-ticker-> eicon ow asche icon to show on elelmentor
	}

	public function get_categories() {
		return [ 'chariton-elements' ];    // category of the widget
	}
     public function get_script_depends() {
		return [ 'chariton-elementor-editor' ];
	}

	/**
	 * A list of scripts that the widgets is depended in
	 * @since 1.3.0
	 **/
protected function _register_controls() {
		
	//start of a control box
		$this->start_controls_section(
			'section_content',
			[
				'label' => esc_html__( 'Testimonial', 'chariton' ),   //section name for controler view
			]
		);
	
		$this->add_control(
			'post_number',
			[
				'label' => esc_html__( 'Number of testimonial', 'chariton' ),
				'description' => esc_html__( 'Give -1 for all post', 'chariton' ),
				'type' => Controls_Manager::NUMBER,
				'default' => 3,
			]
		);
		$this->add_control(
			'orderby',
			[
				'label' => __( 'Order by', 'chariton' ),
				'type' => Controls_Manager::SELECT,
				'default' => 'date',
				'options' =>ifinger_post_orderby_options(),
			]
		);
		$this->add_control(
			'order',
			[
				'label' => __( 'Order', 'chariton' ),
				'type' => Controls_Manager::SELECT,
				'default' => 'DESC',
				'options' => [
					'ASC' => __( 'Ascending Order', 'chariton' ),
					'DESC' => __( 'Descending', 'chariton' ),
				],
			]
		);

		$this->add_control(
			  'review_disable',
			  [
			     'label'       => __( 'Review Disable ?', 'chariton' ),
			     'type' => Controls_Manager::SELECT,
			     'default' => 'no',
			     'options' => [
			     	'no' => __( 'No', 'chariton' ),
			     	'yes'  => __( 'Yes', 'chariton' ),
			     ],
			  ]
		);


		$this->add_control(
			  'slider',
			  [
			     'label'       => __( 'Slider', 'chariton' ),
			     'type' => Controls_Manager::SELECT,
			     'default' => 'no',
			     'options' => [
			     	'no' => __( 'No', 'chariton' ),
			     	'yes'  => __( 'Yes', 'chariton' ),
			     ],
			  ]
		);

		$this->add_control(
			'show_item',
			[
			    'label'       => __( 'Show on large device', 'chariton' ),
			    'type' => Controls_Manager::SELECT,
			    'default' => '4',
			    'options' => [
			     	'2'  => __( '2', 'chariton' ),
			     	'3' => __( '3', 'chariton' ),
			     	'4' => __( '4', 'chariton' ),
			     	'6' => __( '6', 'chariton' ),
			    ],
			    'condition' => [
					'slider' => 'yes',
				],
			]
		);
		$this->add_control(
			'show_desktop',
			[
			    'label'       => __( 'Show on desktop', 'chariton' ),
			    'type' => Controls_Manager::SELECT,
			    'default' => '3',
			    'options' => [
			     	'2'  => __( '2', 'chariton' ),
			     	'3' => __( '3', 'chariton' ),
			     	'4' => __( '4', 'chariton' ),
			     	'5' => __( '5', 'chariton' ),
			    ],
			    'condition' => [
					'slider' => 'yes',
				],
			]
		);
		$this->add_control(
			'show_tablet',
			[
			    'label'       => __( 'Show on Tablet', 'chariton' ),
			    'type' => Controls_Manager::SELECT,
			    'default' => '2',
			    'options' => [
			     	'2'  => __( '2', 'chariton' ),
			     	'3' => __( '3', 'chariton' ),
			     	'4' => __( '4', 'chariton' ),
			     	'5' => __( '5', 'chariton' ),
			    ],
			    'condition' => [
					'slider' => 'yes',
				],
			]
		);
		$this->add_control(
			'show_tab',
			[
			    'label'       => __( 'Show on tab', 'chariton' ),
			    'type' => Controls_Manager::SELECT,
			    'default' => '1',
			    'options' => [
			     	'1'  => __( '1', 'chariton' ),
			     	'2'  => __( '2', 'chariton' ),
			     	'3' => __( '3', 'chariton' ),
			    ],
			    'condition' => [
					'slider' => 'yes',
				],
			]
		);
		$this->add_control(
			'show_phone',
			[
			    'label'       => __( 'Show on phone', 'chariton' ),
			    'type' => Controls_Manager::SELECT,
			    'default' => '1',
			    'options' => [
			     	'1' => __( '1', 'chariton' ),
			     	'2' => __( '2', 'chariton' ),
			     	'3' => __( '3', 'chariton' ),
			    ],
			    'condition' => [
					'slider' => 'yes',
				],
			]
		);

		$this->end_controls_section();
	}


	protected function render() {				//to show on the fontend 
		$settings = $this->get_settings();

		$post_number = $settings['post_number'];
		$orderby = $settings['orderby'];
		$order = $settings['order'];

		$review_disable = $settings['review_disable'];
		$slider = $settings['slider'];
		$show_item = $settings['show_item'];
		$show_desktop = $settings['show_desktop'];
		$show_tablet = $settings['show_tablet'];
		$show_tab = $settings['show_tab'];
		$show_phone = $settings['show_phone'];


		$grid_query= null;
	    $args = array(
	       'post_type'      => 'testimonial',
	       'post_status'    => 'publish',
	       'orderby' => $team_orderby,
	       'order' => $team_order,
	       'posts_per_page' => $post_number,
	    );
		 
		$grid_query = new \WP_Query( $args );

		if ( $grid_query->have_posts() ) : 


	if ( $slider == 'yes' ) {

		$e_uniqid     = uniqid();
?>

<script type="text/javascript">
    jQuery(document).ready(function(){

		// testimonial-active
		jQuery(<?php echo "'.testi-slider-$e_uniqid'"; ?>).slick({
		  dots: false,
		  infinite: true,
		  speed: 600,
		  prevArrow: '<button type="button" class="slick-prev"><i class="far fa-angle-left"></i></button>',
		  nextArrow: '<button type="button" class="slick-next"><i class="far fa-angle-right"></i></button>',
		  arrows: true,
		  centerMode: true,
		  centerPadding: '145px',
		  slidesToShow: <?php echo esc_attr( $show_item ); ?>,
		  slidesToScroll: 1,
		  responsive: [
		    {
		      breakpoint: 1700,
		      settings: {
		        slidesToShow: <?php echo esc_attr( $show_desktop ); ?>,
				slidesToScroll: 1,
				centerPadding: '200px',
		      }
		    },
		    {
		      breakpoint: 1500,
		      settings: {
		        slidesToShow: <?php echo esc_attr( $show_tablet ); ?>,
				slidesToScroll: 1,
				centerPadding: '260px',
		      }
		    },
		    {
		      breakpoint: 1200,
		      settings: {
		        slidesToShow: <?php echo esc_attr( $show_tab ); ?>,
				slidesToScroll: 1,
				centerPadding: '100px',
		      }
		    },
		    {
		      breakpoint: 992,
		      settings: {
		        slidesToShow: <?php echo esc_attr( $show_tab ); ?>,
				slidesToScroll: 1,
				centerPadding: '0px',
		      }
		    },
		    {
		      breakpoint: 767,
		      settings: {
		        slidesToShow: <?php echo esc_attr( $show_phone ); ?>,
		        slidesToScroll: 1,
				arrows: false,
				centerPadding: '100px',
		      }
		    },
		    {
		      breakpoint: 575,
		      settings: {
		        slidesToShow: <?php echo esc_attr( $show_phone ); ?>,
		        slidesToScroll: 1,
				arrows: false,
				centerPadding: '0px',
		      }
		    },
		  ]
		});

    });
</script> 

<div class="row <?php echo "testi-slider-$e_uniqid"; ?> testimonial-active">
	<?php while ( $grid_query->have_posts() ) : $grid_query->the_post(); global $post; 

	    $ifinger_testimonial_info = get_post_meta( get_the_ID(), '_ifinger_testimonial', true );

	    if (!empty($ifinger_testimonial_info['designation'])) {
	      $designation = $ifinger_testimonial_info['designation'];
	    } else {
	      $designation = '';
	    }if (!empty($ifinger_testimonial_info['rewiew_setting'])) {
	      $rewiew_setting = $ifinger_testimonial_info['rewiew_setting'];
	    } else {
	      $rewiew_setting = '';
	    }if (!empty($ifinger_testimonial_info['rewiew_color'])) {
	      $rewiew_color = $ifinger_testimonial_info['rewiew_color'];
	    } else {
	      $rewiew_color = '';
	    }
  	?>
    <div class="col-xl-4">
        <div class="single-testimonial">
            <?php if( $review_disable != 'yes' ){ ?>
      		<div class="testi-review mb-15">
      			<?php 
      			  for ($i=0; $i <=4 ; $i++) {
      			    if ($i < $rewiew_setting) {
      			      $full = 'fas';
      			    } else {
      			      $full = 'far';
      			    }
      			    echo "<i class=\"$full fa-star\"></i>";
      			  }
      			?>
      		</div>
          	<?php } ?>

            <div class="testi-content">
                <?php the_content(); ?>
            </div>
            <div class="testi-avatar">
                <h4><?php the_title(); ?></h4>
                <span><?php echo esc_html( $designation ); ?></span>
            </div>
            <i class="fal fa-quote-left"></i>
        </div>
    </div>

    <?php endwhile; wp_reset_postdata(); ?>
</div>

<?php } else { ?>

<div class="row testimonial-grid">
	<?php while ( $grid_query->have_posts() ) : $grid_query->the_post(); global $post; 

	    $ifinger_testimonial_info = get_post_meta( get_the_ID(), '_ifinger_testimonial', true );

	    if (!empty($ifinger_testimonial_info['designation'])) {
	      $designation = $ifinger_testimonial_info['designation'];
	    } else {
	      $designation = '';
	    }if (!empty($ifinger_testimonial_info['rewiew_setting'])) {
	      $rewiew_setting = $ifinger_testimonial_info['rewiew_setting'];
	    } else {
	      $rewiew_setting = '';
	    }if (!empty($ifinger_testimonial_info['rewiew_color'])) {
	      $rewiew_color = $ifinger_testimonial_info['rewiew_color'];
	    } else {
	      $rewiew_color = '';
	    }
  	?>
    <div class="col-xl-4">
        <div class="single-testimonial">
            <?php if( $review_disable != 'yes' ){ ?>
      		<div class="testi-review mb-15">
      			<?php 
      			  for ($i=0; $i <=4 ; $i++) {
      			    if ($i < $rewiew_setting) {
      			      $full = 'fas';
      			    } else {
      			      $full = 'far';
      			    }
      			    echo "<i class=\"$full fa-star\"></i>";
      			  }
      			?>
      		</div>
          	<?php } ?>

            <div class="testi-content">
                <?php the_content(); ?>
            </div>
            <div class="testi-avatar">
                <h4><?php the_title(); ?></h4>
                <span><?php echo esc_html( $designation ); ?></span>
            </div>
            <i class="fal fa-quote-left"></i>
        </div>
    </div>
    <?php endwhile; wp_reset_postdata(); ?>
</div>

<?php } endif;   //main if end

	}

}
